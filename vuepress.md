* 安装
  
  > cnpm install -g vuepress
  >
  > cnpm i vuepress-init -g
  > vuepress init
  > cd <your project> && npm install
  >
  > npm install vuepress-theme-yubisaki@next --save-dev //install theme
  >
  > npm run dev

* System limit for number of file watchers reached

  > sudo vi /etc/sysctl.conf
  >
  > 在最下添加
  >
  > fs.inotify.max_user_watches=524288
  >
  > 保存退出
  >
  > sudo sysctl -p