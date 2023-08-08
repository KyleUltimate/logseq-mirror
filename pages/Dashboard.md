- {{renderer :kanban_encgmikj}}
	- tasks
		- #+BEGIN_QUERY
		  {:title [:h3 "Tasks" ]
		  :query [:find (pull ?b [*])
		  :where
		    [?b :block/marker ?marker]
		    [(missing? $ ?b :block/scheduled)]
		    [?b :block/page ?page]
		    [?page :block/original-name ?name]]
		  :breadcumb-show? false
		  :result-transform (fn [result]
		  (sort-by (fn [h]
		  (get h :block/created-at)) result))
		  :collapsed? false
		  }
		  #+END_QUERY
- #+BEGIN_QUERY
  {:title "All pages have a *programming* tag"
   :query [:find ?name
         :in $ ?tag
         :where
         [?t :block/name ?tag]
         [?p :block/tags ?t]
         [?p :block/name ?name]]
   :inputs ["daily_words"]
   :view (fn [result]
         [:div.flex.flex-col
          (for [page result]
            [:a {:href (str "#/page/" page)} (clojure.string/capitalize page)])])}
  #+END_QUERY