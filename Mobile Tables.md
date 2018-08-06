# CSS Trick

Fond in Mow reports - Repeat

Changes to table

1. in the div surounding the table add the id of 'no-more-tables'
2. Each TD needs a data-title="Care" where Care is the field label

Add the following CSS global

````
// START No-More-Tables
// Found in https://elvery.net/demo/responsive-tables/
@media only screen and (max-width: 800px) {

  /* Force table to not be like tables anymore */
  #no-more-tables table,
  #no-more-tables thead,
  #no-more-tables tbody,
  #no-more-tables th,
  #no-more-tables td,
  #no-more-tables tr {
    display: block;
  }

  /* Hide table headers (but not display: none;, for accessibility) */
  #no-more-tables thead tr {
    position: absolute;
    top: -9999px;
    left: -9999px;
  }

  #no-more-tables tr {
    border: 1px solid #ccc;
  }

  #no-more-tables td {
    /* Behave  like a "row" */
    border: none;
    border-bottom: 1px solid #eee;
    position: relative;
    padding-left: 50%;
    white-space: normal;
    text-align: left;

  }

  #no-more-tables td:before {
    /* Now like a table header */
    position: absolute;
    /* Top/left values mimic padding */
    top: 6px;
    left: 6px;
    width: 45%;
    padding-right: 10px;
    white-space: nowrap;
    text-align: left;
    font-weight: bold;

  }

  /*
  Label the data
  */
  #no-more-tables td:before {
    content: attr(data-title);
  }
}

// End No-More-Tables
````

Found reference in [Responsive Tables Demo - No More Tables](https://elvery.net/demo/responsive-tables/)

Article on [Responsive Data Tables](https://css-tricks.com/responsive-data-tables/) By CHRIS COYIER.

## Desktop Size



## Phone Size



