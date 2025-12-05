Notes

```oc patch ingresscontroller/default -n openshift-ingress-operator \
  --type=merge \
  --patch='{"spec":{"logging":{"access":{"destination":{"type":"Container"},"httpLogFormat":"%ci:%cp [%tr] %ft %b/%s %TR/%Tw/%Tc/%Tr/%Ta %ST %B %CC %CS %tsc %ac/%fc/%bc/%sc/%rc %sq/%bq %hr %hs {%[capture.req.hdr(0)]} %{+Q}r"}}}}'
```

**Key fields in the log format:**
- `%ci` = **Client IP** (the real source IP you want)
- `%cp` = Client Port
- `%ft` = Frontend name (route)
- `%b` = Backend name (service)
- `%ST` = Status code
- `%r` = HTTP request

### **Example Log Output:**
```
192.168.1.100:54321 [04/Dec/2025:10:30:45.123] public be_http:my-namespace:my-app/pod:my-app-pod-abc:my-app:8080 0/0/1/2/3 200 1234 - - ---- 1/1/0/0/0 0/0 "GET /api/users HTTP/1.1"
