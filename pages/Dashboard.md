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
-
-
- #+BEGIN_QUERY
  {:title [:h3 "Tasks" ]
  :query [:find (pull ?b [*])
  :where
    [?b :block/marker ?marker]
    [(not= ?marker "DONE")]
    [(missing? $ ?b :block/scheduled)]
    [?b :block/page ?page]
    [?page :block/original-name ?name]
    [(get-else $ ?b :block/updated ?updated (now))]
    [(> 1 (days-between (now) ?updated))]
  ]
  :breadcumb-show? false
  :collapsed? false
  }
  #+END_QUERY