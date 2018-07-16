This s a discussion on how to disable the button first and then do the long running process.


See https://github.com/vuejs/Discussion/issues/297
Example at the bottom:

````
var vue = new Vue({
    el: '#app',
   
    methods: {
        calculate: function(){
            event.preventDefault();
			      event.target.disabled = true;
            setTimeout(function(){
				        var i=0;
				        for (i=0; i<1500000000; i++);
                console.log(i);
            }, 1)
        }
    }
});
````
