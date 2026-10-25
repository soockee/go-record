# Agent instructions

## Project

`go-record` is a reusable Go library for Windows WASAPI capture and rendering. Keep its public API and documented behavior compatible unless the issue explicitly requests a breaking change.

## Toolchain and validation

- Use Go 1.27.3. The `go.mod` toolchain directive and GitHub Actions workflow pin this version.
- Run `gofmt -w` on changed Go files.
- Run `go vet ./...`, `go test -shuffle=on -count=1 ./...`, and `go build ./...` before proposing a change.
- WASAPI behavior needs Windows and audio hardware for full manual validation. State clearly when that validation was unavailable; do not claim a hardware test passed based only on compilation.

## Agent task boundaries

- Work only on the issue's stated behavior and acceptance criteria.
- Treat device access, COM lifetimes, stream shutdown, and concurrency as sensitive areas. Preserve cancellation behavior and avoid introducing goroutine leaks.
- For changes that also require `go-tuner`, document the API contract and the expected dependency/release order. Do not edit or commit the other repository from this task unless the issue explicitly requests a coordinated change.
- Iterate against failing checks at most three focused repair rounds. If the same check still fails, stop, report the evidence, and leave a reviewable draft rather than weakening or deleting the check.
- Do not publish a release, merge a pull request, or deploy software. Prepare reviewable changes and report any required release steps.
