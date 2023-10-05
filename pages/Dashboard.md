template:: Todo List

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
		  :collapsed? false
		  }
		  #+END_QUERY
- #+BEGIN_QUERY
  {:title [:h3 "Tasks" ]
  :query [:find (pull ?b [*])
  :where
    [?b :block/marker ?marker]
    [(contains? #{"NOW" "LATER" "DONE"} ?marker)]
    [?b :block/page ?page]
    [?page :block/original-name ?name]
    [?b :block/marker ?marker]
  ]
  :breadcumb-show? false
  :collapsed? false
  }
  #+END_QUERY