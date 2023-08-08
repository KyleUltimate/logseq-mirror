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
- {{query #daily_words}}
- #+BEGIN_QUERY
  {:title [:h3 "Tasks" ]
  :query [:find (pull ?b [*])
  :in $ ?tag
  :where
    [?t :block/name ?tag]
    [?p :block/tags ?t]
    [?b :block/page ?page]
    [?p :block/name ?name]
    [?page :block/original-name ?name]]
  :breadcumb-show? false
  :result-transform (fn [result]
  (sort-by (fn [h]
  (get h :block/created-at)) result))
  :collapsed? false
  }
  #+END_QUERY