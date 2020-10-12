# indec.js
var download = require('download-git-repo')

/**
 * Expose `cli`
 */

exports.cli = cli

/**
 * Show help message
 */

function help () {
  console.log('')
  console.log('Usage')
  console.log('  $ download-git-repo <url>')
  console.log('  $ download-git-repo <url> <directory>')
  console.log('  $ download-git-repo <url> <directory> --clone')
  console.log('')
  console.log('Example')
  console.log('  $ download-git-repo -h')
  console.log('  $ download-git-repo flippidippi/download-git-repo-fixture')
  console.log('  $ download-git-repo flippidippi/download-git-repo-fixture test/tmp')
  console.log('  $ download-git-repo gitlab:flippidippi/download-git-repo-fixture')
  console.log('  $ download-git-repo gitlab:custom.com:flippidippi/download-git-repo-fixture')
  console.log('  $ download-git-repo bitbucket:flippidippi/download-git-repo-fixture#my-branch test/tmp --clone')
  console.log('')
  console.log('Options')
  console.log('  -h, --help          Show help')
  console.log('  -c, --clone         Use git clone instead of an http download.')
  console.log('')
}

/**
 * Run download-git-repo from CLI
 * download-git-repo src [dest] [--clone | -c]
 */

function cli () {
  var argv = require('yargs')
    .boolean('c')
    .boolean('h')
    .alias('c', 'clone')
    .alias('h', 'help')
    .argv

  if (argv.h) return help()

  var src = argv._[0]
  var dest = argv._[1] || process.cwd()
  var options = {}

  if (argv.c) options.clone = true

  download(src, dest, options, function (err) {
    if (err) console.log(err)
  })
}
