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
    [(missing? $ ?b :block/scheduled)]
    [?b :block/page ?page]
    [?page :block/original-name ?name]]
    [?b :block/done false]
    [(> (datomic.api/q '[:find ?date .
                           :in $ ?b
                           :where
                           [?b :block/created ?date]]
                         (datomic.api/db conn) ?b)
        (clojure.core/-> (java.util.Date.)
                          (clojure.core/long)
                          (clojure.core/dec)))]
  :breadcumb-show? false
  :collapsed? false
  }
  #+END_QUERY