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
  {:title "Daily words"
   :query (and [[daily_words]][+Words of the day])
  :breadcumb-show? false
  :result-transform (fn [result] result)
  :collapsed? false
  }
  #+END_QUERY
-