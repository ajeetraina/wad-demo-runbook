# WAD Demo — Commands Cheat Sheet

Commands only, top to bottom. Steps 5–7 need the real provisioned machine.

## Setup (per session)
```sh
cd /Users/ajeetraina/work/wad26/wad-demo-presenter
. runtime/.install-state/env.sh
sbx version
```

## 1. Isolation
```sh
sbx run --name wad-coding-factory
```
At Claude prompt:
```
Describe the project for me.
```

## 2. Kits and environments
```sh
cat runtime/kits/demo-node/spec.yaml
cat runtime/sbxenv.yaml
```

## 3. Working app
```sh
open http://127.0.0.1:3001/
```

## 4. Network and credentials
At Claude prompt:
```
! curl https://github.com/
! curl https://example.org/
```
Optional host contrast:
```sh
curl https://example.org/
```

## 5. Governance (real machine only)
Browser: network policy, MCP allow/deny, one audit row.

## 6. Cloud sandboxes (real machine only)
```sh
sbx --cloud ls
sbx --cloud attach <prepared-sandbox-id>
```

## 7. Pick up the work (real machine only)
At cloud Claude prompt:
```
What did you change, and how did the tests go?
```
```
! cd /home/agent/wad-cloud-demo && python3 -m unittest -v
```

## 8. DHI / Scout
```sh
sbx exec -it wad-dhi-scout bash
export DHI_IMAGE=dhi.io/node@sha256:61b89b9bd1551723b56de57bf41cc62daeffb266d80636a83cf6b85e35bf17d1
docker run --rm --network none "$DHI_IMAGE" node --version
docker scout quickview "$DHI_IMAGE"
docker scout cves --only-severity critical,high "$DHI_IMAGE"
```

## Reset
```sh
cd /Users/ajeetraina/work/wad26/wad-demo-presenter
./demo reset
```

## Verify
```sh
cd /Users/ajeetraina/work/wad26/wad-demo-presenter
. runtime/.install-state/env.sh
./demo check --model
```
