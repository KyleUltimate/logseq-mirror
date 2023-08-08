- {{renderer :kanban_iflhrirda}}
	- tasks
		- #+BEGIN_QUERY
		  {:title [:h3 "Tasks" ]
		  :query [:find (pull ?b [*])
		  :where
		    [?b :block/marker ?marker]
		  [(contains? #{"TODO" "DOING" "DONE"} ?marker)]
		  ]
		  }
		  #+END_QUERY
- :LOGBOOK:
  CLOCK: [2023-08-08 Tue 10:24:29]
  :END: