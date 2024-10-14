# Permission Denied

## Q: Why do I get a "permission denied" error when using Docker commands, even with `sudo`?

**A**: Try restarting Docker services using the following command:

```bash
sudo systemctl restart docker.socket docker.service
```

## Reference

- [Error response from daemon: Cannot kill container: permission denied, how to kill docker containers on Ubuntu 20.04? - Stack Overflow](https://stackoverflow.com/questions/71477749/error-response-from-daemon-cannot-kill-container-permission-denied-how-to-kil)
