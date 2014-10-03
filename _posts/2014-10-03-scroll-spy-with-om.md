---
layout: default
title: Hello world
comments: true
---

Scroll Spy with OM
==================

Scroll Spy's are helpful little widgets which give user feedback about their
position on a page. Typically they are a fixed navbar that is always visible
regardless of scroll position. As the user scrolls the active link list
changes to give feedback. The ever popular Twitter Bootstrap's documentation
is a fine example of this. As you scroll the sidebar shows your position.
http://getbootstrap.com/components

This is quite simple to create in plain clojurescript without any calls to
external libraries like jQuery.

Let's get stuck in!

```clojure
(defcomponentk list [[:data list :as app] state owner]
  (render [_]
    (html
      [:div
        [:table
          [:thead
            [:tr [:th "Name"]]]
          (for [[group items] (group-by (comp first :name) list)]
            [:tbody {:id group}
              (for [item items]
                [:tr
                  [:td item]])])]])))
```

This simple om component takes a list of like `[{:name "foo"} {:name "bar"}]`
and renders the list as a table where all items are grouped by the first
letter of their name. Each of these groups is a `<tbody>` with the id being
the first letter.

Let's create a component which can be given a list of ids `["A" "B" "C" ...]`
and render a navigation bar.

```clojure
(defcomponentk nav [[:data ids] state owner]
  (render [_]
    [:div.nav
      [:ul
        (for [id ids]
          [:li [:a {:href (str "#" id)} id]])]]))
```

Let's update the list component to show the nav component.

```clojure
(defcomponentk list [[:data list :as app] state owner]
  (render [_]
    (html
      [:div
        (->nav {:ids ["A" "B" "C" "D" "E]})
        [:table
          [:thead
            [:tr [:th "Name"]]]
          (for [[group items] (group-by (comp first :name) list)]
            [:tbody {:id group}
              (for [item items]
                [:tr
                  [:td item]])])]])))
```
Now let's create a random list and mount the component:

```clojure
(def data (map #({:name (apply str (shuffle "ABCDE"))})
               (range 1 30)))

(om/root list {:list data}
              {:target (.-body js/document)})
```
Pretty simple so far... But nothing happens when we scroll yet.
Let's hook in an event listener! Add the following did-mount block to
the nav component.

```clojure
(did-mount [_]
  (events/listen js/window
                 goog.events.EventType.SCROLL
                 #(println
                     (map (fn [x]
                            [x
                             (- (.-offsetTop (.getElementById js/document x))
                                (.pageYOffset js/window))])
                          ids))))
```

Now scroll the page. You should see the id and its relative position
from the top of the page being printed out to the console. The closer the value
is to zero the closer it is to the top of the page. Positive values have scrolled
north out of the view port.

Let's set the nav's local state to reflect be the id which is closest to the
top.

Add an `init-state` to the component:

```clojure
(init-state [_]
  {:active nil})
```

Change the `did-mount` block to handle updating the state:

```clojure
(did-mount [_]
  (events/listen js/window
                 goog.events.EventType.SCROLL
                 #(->> ids
                       (map (fn [x]
                               [x (- (.-offsetTop
                                      (.getElementById js/document x))
                                     (.pageYOffset js/window))]))
                       (filter (comp neg? second))
                       (sort-by second >)
                       (ffirst)
                       (swap! state assoc :active)))
```

Here we use clojure's thread last macro to construct a list processing
pipeline which would have otherwise been an ugly nested piece of code.

We take our ids and get there distances from the top of the page.
We keep any negative ones - `(comp neg? second)` is the same as
`#(neg? (second %))`.

We then sort all the ids by there position and take first elements
id `ffirst` is the same as `#(first (first %))`.

Let's allow the render block to reflect the active state by changing the styling of the links when they are active:

```clojure
[:li
  [:a {:href (str "#" id)
       :class (when (= (:active @state) id)
                "active")}
    id]]
```

Checkout the full code [here](github.com)
