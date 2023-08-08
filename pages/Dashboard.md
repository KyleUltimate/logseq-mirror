- {{renderer :kanban_lztiuhuc}}
	- Todo
		- Later
			- #+BEGIN_QUERY
			  {:title [:h3 "Main Tasks:]
			  :query [:find (pull ?b [*])]
			  :where
			  [?b :block/marker ?marker]
			  [(missing? $ ?b :block/scheduled]
			  [?b :block/page ?page]
			  [?page :block/original-name ?name]
			  :breadcumb-show? false
			  :result-transform (fn [result]
			  )
			  :collapsed? false
			  }
			  #+END_QUERY
		- In progress
			- {{query (todo now)}}
- NOW FUCK MYSELF
  :LOGBOOK:
  CLOCK: [2023-08-08 Tue 10:15:35]
  CLOCK: [2023-08-08 Tue 10:15:37]
  CLOCK: [2023-08-08 Tue 10:15:37]
  :END:
- /k