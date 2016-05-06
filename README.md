# support-ship
Anything related to implementation or migration of support sites

Site theme demo: http://www.mojo-themes.com/item/docs-responsive-documentation-wordpress-theme/demo/

Added the following to .../wp-content/themes/docs/templates/head.php, just inside `</head>`

 
```
<script>
   (function () {
      var head = document.getElementsByTagName("head").item(0);
      var script = document.createElement("script");
      var src = (document.location.protocol == 'https:' ? 'https://www.formilla.com/scripts/feedback.js' : 'http://www.formilla.com/scripts/feedback.js');
      script.setAttribute("type", "text/javascript"); script.setAttribute("src", src); script.setAttribute("async", true);
      var complete = false;

      script.onload = script.onreadystatechange = function () {
          if (!complete && (!this.readyState || this.readyState == 'loaded' || this.readyState == 'complete')) {
              complete = true;
              Formilla.guid = '<guid>';
              Formilla.loadFormillaChatButton();
          }
      };

      head.appendChild(script);
  })();
    
  jQuery(document).ready(function($) {
    $(".nav-main #menu .menu-live-chat").on("click", function(e){
      if(typeof Formilla != 'undefined') {
        Formilla.initFormillaChat();
      }
    });
  });
  </script>
```
