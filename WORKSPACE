workspace(
  name = "dsfx3d",
)

load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
  name = "aspect_rules_js",
  sha256 = "9fadde0ae6e0101755b8aedabf7d80b166491a8de297c60f6a5179cd0d0fea58",
  strip_prefix = "rules_js-1.20.0",
  url = "https://github.com/aspect-build/rules_js/releases/download/v1.20.0/rules_js-v1.20.0.tar.gz",
)

load("@aspect_rules_js//js:repositories.bzl", "rules_js_dependencies")

rules_js_dependencies()

load("@rules_nodejs//nodejs:repositories.bzl", "DEFAULT_NODE_VERSION", "nodejs_register_toolchains")

nodejs_register_toolchains(
  name = "nodejs",
  node_version = "18.12.0",
)

load("@aspect_rules_js//npm:npm_import.bzl", "npm_translate_lock")

npm_translate_lock(
  name = "npm",
  data = ["//:package.json"],
  patch_args = {
    "*": ["-p1"],
  },
  pnpm_lock = "//:pnpm-lock.yaml",
  pnpm_version = "7.17.1",
  update_pnpm_lock = True,
  verify_node_modules_ignored = "//:.bazelignore",
)

load("@npm//:repositories.bzl", "npm_repositories")

npm_repositories()

http_archive(
  name = "aspect_rules_ts",
  sha256 = "db77d904284d21121ae63dbaaadfd8c75ff6d21ad229f92038b415c1ad5019cc",
  strip_prefix = "rules_ts-1.3.0",
  url = "https://github.com/aspect-build/rules_ts/releases/download/v1.3.0/rules_ts-v1.3.0.tar.gz",
)

##################
# rules_ts setup #
##################
# Fetches the rules_ts dependencies.
# If you want to have a different version of some dependency,
# you should fetch it *before* calling this.
# Alternatively, you can skip calling this function, so long as you've
# already fetched all the dependencies.
load("@aspect_rules_ts//ts:repositories.bzl", "LATEST_VERSION", "rules_ts_dependencies")

rules_ts_dependencies(
  # This keeps the TypeScript version in-sync with the editor, which is typically best.
  ts_version_from = "//:package.json",

  # Alternatively, you could pick a specific version, or use
  # load("@aspect_rules_ts//ts:repositories.bzl", "LATEST_VERSION")
  # ts_version = LATEST_VERSION
)
