- {{renderer :kanban_iflhrirda}}
	- tasks
		- #+BEGIN_QUERY
		  {:title [:h3 "Tasks" ]
		  :query [:find (pull ?b [*])
		  :where
		    [?b :block/marker ?marker]
		    [(missing? $ ?b: block/scheduled)]
		    [?b :block/page ?page]
		    [?page :block/original-name ?name]]
		  }
		  #+END_QUERY
-
-