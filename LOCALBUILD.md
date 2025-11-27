## How to build the site locally

The following approach will let you build the site locally using Jekyll in a Podman container (to keep the host machine clean)

### Preparation

The `jekyll serve` command we want to run requires the `webrick` gem, but we have no Gemfile in the repo. Accordingingly, create one:

```
cat <<EOF > Gemfile
source "https://rubygems.org"

gem "github-pages", group: :jekyll_plugins
gem "webrick"
EOF
```

We also need to make the working dir writable by the container. This isn't ideal, but it'll work:
```
chmod 777 .
```

Now we can get rolling: 

```
podman run --rm -it -p 4000:4000 -v "$PWD:/srv/jekyll:Z" docker.io/jekyll/jekyll jekyll serve --host 0.0.0.0
```

Then http://localhost:4000 should work on your host machine
