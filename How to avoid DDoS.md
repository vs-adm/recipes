## Collect atackers IP

```bash
tail -f /tmp2/access.log | awk '{print $11}' > ~/iplist
```

## Convert access log into IP list sorted by requests

```bash
cat iplist | \
cut -c 2- | rev | cut -c 2- | rev | \
sort | uniq -c | sort -rn | \
head -n 40 | awk '{print $2}' > ~/uniq_ips
```

## Ban every IP

```bash
for i in `cat ~/uniq_ips`; do iptables -I INPUT 1 -s $i -j DROP; done
```
