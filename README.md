# `cth_retry`

An experimental OTP library to be used to generate Common Test test
specifications for the latest failing test cases so they can be retried easily.

I'm still experimentating with ways to make it more usable and possibly turning
this into a rebar3 plugin.

## Usage

Add the following to your `rebar.config`:

```erlang
{profiles, [
    {test, [
        {deps, [
            {cth_retry, {git, "https://github.com/ferd/cth_retry.git", {branch, "master"}}}
        ]}
    ]}
]}.

{ct_opts, [{ct_hooks, [cth_retry]}]}.
```

Run your tests:

```
$ rebar3 ct
...
Writing retry specification at /home/ferd/code/self/cth_readable/_build/test/logs/retry.spec
Failed 3 tests. Passed 1 tests.
Results written to "/home/ferd/code/self/cth_readable/_build/test/logs/index.html".
===> Failures occurred running tests: 3
...
```

On any failure, a list of the failed test cases will be put in a retry.spec
file that can be called independently:

```
$ rebar3 ct --spec _build/test/logs/retry.spec
...
```

This invocation will then re-run the failing tests only and none of the rest.


## Changelog

0.1.0:
- First demo.

