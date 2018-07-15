# Doc

https://github.com/axios/axios

# Install

````
npm install axios --save
````

# Quick Example

````
<script>
 
  import axios from 'axios';  
        .
        .
        .

loadData: function () {

var self = this;

var url = self.getDataUrl();

axios.get(url)
    .then(function (response) {
            
        var data = response.data;
            
        console.log(data);
            
        self.gridData = data.data;
        self.total = data.total;
    })    
    .catch(function (error) {
        console.log(error);
    });   
},        
````

# Progress Bar

* https://www.htmlgoodies.com/beyond/php/show-progress-report-for-long-running-php-scripts.html
