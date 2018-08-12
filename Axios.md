# Doc

https://github.com/axios/axios

# Install

````
npm install axios --save
````

# Quick Example
Not use of `=>` keeping us away from the `self.` stuf or using `bind()`

````

 import axios from 'axios';  
 
      save() {
        axios.post('/work-order/' + this.params.work_order_id + '/add-log', this.PostData)
          .then(responce => {
            this.WorkOrderLogId = responce.data.work_order_log_id;
            this.SaveWoImages = responce.data.work_order_log_id;
            this.my_message = responce.data.message;
          })
          .catch(error => {
            if (error.response && error.response.status == 422) {
              this.fld_errors = error.response.data.errors;
            } else {
              this.global_error_message = 'Error, please try again. If error persists please report.'
            }

          });
      },
````      


# Another Quick example

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
