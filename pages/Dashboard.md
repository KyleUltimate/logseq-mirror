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
  {:query [:find (pull ?b [*])
  :in $ ?start ?next 
  :where
      [?b :block/marker ?m]
      [(contains? #{"TODO" "DOING"} ?m)]
      (or [?b :block/scheduled ?d] [?b :block/deadline ?d])
      [(>= ?d ?start)]
        [(<= ?d ?next)]]
  :inputs [:30d-before :today]
  :result-transform (fn [result]
      (sort-by (fn [h] (get-in h [:block/content])) result))
  :breadcrumb-show? false
  :table-view? false
  }
  #+END_QUERY