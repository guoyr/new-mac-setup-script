### How to Run MMS Automation Tests Locally

#### On Mac and Ubuntu 12.04

1. Install Go v1.3 or later: https://golang.org/doc/install. 

   After installation, run `go version` to verify that you have v1.3 or later

2. Request access to the MMS Automation repository (if you don’t have it already)

   Clone the repository: `git clone git@github.com:10gen/mms-automation.git`


3. Set the `GOPATH` and `CM_ROOT` environment variables to the `go_planner` subdirectory of the automation repository.  For example, if you cloned automation into `~/mms-automation`, your environment variables would be:

```sh
export GOPATH=${HOME}/mms-automation/go_planner
export CM_ROOT=${HOME}/mms-automation/go_planner
```

4. Run `gpm` inside the automation repository:

```sh
cd ~/mms-automation
./gpm
```

5. Run the test suite of your choice located in `go_planner/src/com.tengen/cm/fulltest`.  Each file is generally a test suite containing multiple tests. The function declarations for each test look like the following example:

```go
func (s *AuthFullSuite) TestAuth26(c *C)
```

where `AuthFullSuite` is the suite and the function `TestAuth26` is the test (each test begins with "Test").  To run this specific test, type:

```go
cd go_planner/src/com.tengen/cm/fulltest
go test -slow -gocheck.vv -timeout=60m -gocheck.f=AuthFullSuite.TestAuth26
```

To run all the tests in a suite, just leave off the test name and preceding period:

```go
go test -slow -gocheck.vv -timeout=60m -gocheck.f=AuthFullSuite
```

