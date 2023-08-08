- {{renderer :kanban_iflhrirda}}
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
-
-
- NOW FUCK
  :LOGBOOK:
  CLOCK: [2023-08-08 Tue 10:29:44]
  CLOCK: [2023-08-08 Tue 10:29:44]
  :END:
-