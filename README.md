hogan
=====

a builder for easy to use REST API connection. wrestling with rest




Example usage
=============

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
		
			methods : {
				
				doWork : function(attr1, attr2) {
				
					/* do stuff */
				}
			}
			
			noun2 : {
			
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

root.getNoun1(key1, function(noun1) {

	noun1.getNoun2(key2, function(noun2) {
	
		noun2.doWork();
		
		noun1[key1].noun2[key2].doWork();
		
		console.log(noun1.id);		
	};
	
	noun1.getAllNoun2(function(noun2Collection) {
	
		for(var i=0; i<noun2Collection.length; i++) {
		
			console.log(noun2Collection[i].id);
		}
	});
};
