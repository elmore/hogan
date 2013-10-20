hogan
=====

a builder for easy to use REST API connection. wrestling with rest




Example usage
=============

http://www.myhost.com/api/v1/noun1/key1/noun2/key2

configure
---------


	
	var root = Hogan.generate({
		
		name : 'api_one',
		
		protocol : 'http',

		base : 'www.myhost.com/api/v1',
		
		request : function(req) {
		
			/* use whatever ajax lib you like */
		},
				
		domain : {
		
			noun1 : {
				
				// always||never||timed(ms)
				cache : Hogan.cache.always
				
				// triggers hogan to run getAll<noun> on child nodes
				autoPopulate : true,
				
				// become methods on noun1 instances
				methods : {
					
					// user defined method will be attached to all 
					// instances of noun1
					doWork : function(attr1, attr2) {
					
						/* do stuff */
					}
				}
				
				// noun2 objects exist in a collection as a 
				// property of noun1 objects
				noun2 : {
				
					cache : Hogan.cache.expires(1000),
				
					methods : {
					
						doWork : function() {
						
							/* do stuff */
						}
					}
				}	
			}
		}
	});




use
---



	root.api_one.getNoun1(key1, function(noun1) {
		
		// get<noun> is automajically created
		noun1.getNoun2(key2, function(noun2) {
			
			// reference to noun2 has all the methods defined above
			noun2.doWork();
			
			// can also reference absolutely
			root.api_one.noun1[key1].noun2[key2].doWork();
			
			console.log(noun1.id);		
		};
		
		// getAll<noun> is automagically created
		noun1.getAllNoun2(function(noun2Collection) {
		
			for(var i=0; i<noun2Collection.length; i++) {
			
				console.log(noun2Collection[i].id);
			}
		});
	};

	