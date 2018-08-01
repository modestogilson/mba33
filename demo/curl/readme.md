##  How do I measure request and response times at once using cURL?

fonte: [stackoverflow](https://stackoverflow.com/questions/18215389/how-do-i-measure-request-and-response-times-at-once-using-curl)

	curl_time() {
	    curl -so /dev/null -w "\
	   namelookup:  %{time_namelookup}s\n\
	      connect:  %{time_connect}s\n\
	   appconnect:  %{time_appconnect}s\n\
	  pretransfer:  %{time_pretransfer}s\n\
	     redirect:  %{time_redirect}s\n\
	starttransfer:  %{time_starttransfer}s\n\
	-------------------------\n\
	        total:  %{time_total}s\n" "$@"
	}

	$ curl_time -X GET "http://lima:5000/motta/home/1.0.3/temperature/22" -H "accept: text/plain"
	   namelookup:  0.000s
	      connect:  0.000s
	   appconnect:  0.000s
	  pretransfer:  0.000s
	     redirect:  0.000s
	starttransfer:  0.187s
	-------------------------
	        total:  0.187s

	$ curl_time -X GET "http://192.168.10.102:5000/motta/home/1.0.3/devices" -H "accept: text/plain"
	   namelookup:  0.000s
	      connect:  0.000s
	   appconnect:  0.000s
	  pretransfer:  0.000s
	     redirect:  0.000s
	starttransfer:  0.015s
	-------------------------
	        total:  0.015s