---
layout: page
title: "JavaScript date_parse function"
comments: true
sharing: true
footer: true
sidebar: false
alias:
- /functions/view/date_parse:827
- /functions/view/date_parse
- /functions/view/827
- /functions/date_parse:827
- /functions/827
---
<!-- Generated by Rakefile:build -->
A JavaScript equivalent of PHP's date_parse

{% codeblock datetime/date_parse.js lang:js https://raw.github.com/kvz/phpjs/master/functions/datetime/date_parse.js raw on github %}
function date_parse (date) {
  // http://kevin.vanzonneveld.net
  // +   original by: Brett Zamir (http://brett-zamir.me)
  // -    depends on: strtotime
  // *     example 1: date_parse('2006-12-12 10:00:00.5');
  // *     returns 1: {year : 2006, month: 12, day: 12, hour: 10, minute: 0, second: 0, fraction: 0.5, warning_count: 0, warnings: [], error_count: 0, errors: [], is_localtime: false}

  // BEGIN REDUNDANT
  this.php_js = this.php_js || {};
  // END REDUNDANT

  var warningsOffset = this.php_js.warnings ? this.php_js.warnings.length : null;
  var errorsOffset = this.php_js.errors ? this.php_js.errors.length : null;

  try {
    var ts = this.strtotime(date);
  } finally {
    if (!ts) {
      return false;
    }
  }

  var dt = new Date(ts * 1000);

  var retObj = { // Grab any new warnings or errors added (not implemented yet in strtotime()); throwing warnings, notices, or errors could also be easily monitored by using 'watch' on this.php_js.latestWarning, etc. and/or calling any defined error handlers
    warning_count: warningsOffset !== null ? this.php_js.warnings.slice(warningsOffset).length : 0,
    warnings: warningsOffset !== null ? this.php_js.warnings.slice(warningsOffset) : [],
    error_count: errorsOffset !== null ? this.php_js.errors.slice(errorsOffset).length : 0,
    errors: errorsOffset !== null ? this.php_js.errors.slice(errorsOffset) : []
  };
  retObj.year = dt.getFullYear();
  retObj.month = dt.getMonth() + 1;
  retObj.day = dt.getDate();
  retObj.hour = dt.getHours();
  retObj.minute = dt.getMinutes();
  retObj.second = dt.getSeconds();
  retObj.fraction = parseFloat('0.' + dt.getMilliseconds());
  retObj.is_localtime = dt.getTimezoneOffset !== 0;

  return retObj;
}
{% endcodeblock %}

 - [view on github](https://github.com/kvz/phpjs/blob/master/functions/datetime/date_parse.js)
 - [edit on github](https://github.com/kvz/phpjs/edit/master/functions/datetime/date_parse.js)

### Example 1
This code
{% codeblock lang:js example %}
date_parse('2006-12-12 10:00:00.5');
{% endcodeblock %}

Should return
{% codeblock lang:js returns %}
{year : 2006, month: 12, day: 12, hour: 10, minute: 0, second: 0, fraction: 0.5, warning_count: 0, warnings: [], error_count: 0, errors: [], is_localtime: false}
{% endcodeblock %}


### Other PHP functions in the datetime extension
{% render_partial _includes/custom/datetime.html %}
