# ctf_xinetd

> A docker repository for deploying CTF challenges
> 对于一些写代码就是不加“setvbuf”的怎么办？这里提供了一个比较懒人的方法。不知道是不是最好的但是目前能用。
> 改动依赖于stdbuf命令，stdbuf -i0 -o0设置无缓冲区，然后需要添加libstdbu.so到正确位置来实现功能。
> 工程改动是添加一个run.sh和复制lib的位置变化一下。

## Configuration

Put files to floder `bin`. They'll be copied to /home/ctf. **Update the flag** at the same time.

Edit `ctf.xinetd`. replace `./helloworld` to your command.

You can also edit `Dockerfile, ctf.xinetd, start.sh` to custom your environment.

## Build

```bash
docker build -t "helloworld" .
```

DO NOT use *bin* as challenge's name

## Run

```bash
docker run -d -p "0.0.0.0:pub_port:9999" -h "helloworld" --name="helloworld" helloworld
```

`pub_port` is the port you want to expose to the public network.

## Capture traffic

If you want to capture challenge traffic, just run `tcpdump` on the host. Here is an example.

```bash
tcpdump -w helloworld.pcap -i eth0 port pub_port
```
