module GitHub

  extend FileUtils

  REPO_NAME = 'repo'
  MY_USERNAME = 'franklinyu'

  def self.backup(owner:, repo:, branch: 'HEAD')
    source_url = "https://github.com/#{owner}/#{repo}.git"
    backup_url = "git@github.com:#{MY_USERNAME}/#{repo}.git"
    if branch == 'HEAD'
      sh('git', 'clone', source_url, REPO_NAME)
    else
      sh('git', 'clone', '--branch', branch, source_url, REPO_NAME)
    end
    Dir.chdir(REPO_NAME) do
      sh('git', 'remote', 'add', 'backup', backup_url)
      sh('git', 'push', 'backup', branch)
    end
    sh('rm', '-r', '-f', REPO_NAME)
  end

end

task :backup do
  GitHub.backup(owner: 'shadowsocks', repo: 'shadowsocks', branch: 'master')
end