# Error: /var/lib/nginx/body/0000009539" failed (13: Permission denied)

If you see something similar to the following error:

```
2023/12/05 22:45:29 [crit] 6322#6322: *335039 open() "/var/lib/nginx/body/0000009539" 
failed (13: Permission denied), client: ......"
```

That is the correct behavior, in case the request body is larger than the buffer (client_body_buffer_size default 8k|16k),
the whole body or only its part is written to a temporary file (client_body_temp_path).

Try this, change nginx `proxy_temp_path` to `/tmp` and edit your proxy config file:
```
proxy_temp_path /tmp;
```

and restart nginx.
