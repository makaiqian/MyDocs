Linux字體配置
--------

今天Chrome訪問 http://www.freedesktop.org/software/fontconfig/fontconfig-user.html 這頁面時，發現字體的顯示相當的虛。發現chrome默認的字體是Times New Roman，這個字體在ttf-mscorefonts-installer這個包裏，可是microsoft的字體在linux的顯示真是太差了，看來要找一下alternative。經過對比，發現linux libertine這個字體跟Times New Roman差不多，顯示效果要好很多。我沒有修改fontconfig,只是修改了chrome的設置。

然後我發現chrome在顯示Arial這個字體時，效果特別差，我把ttf-mscorefonts-installer裏的Arial這個字體刪除後，發現用的是Liberation Sans，這個字體顯示效果也不好。於是我開始修改fontconfig來換成Droid Sans.


先轉到/etc/fonts/conf.avail下，先看看有哪些配置裏包含Liberation Sans
  grep 'Liberation' *
發現在這個文件裏30-metric-aliases.conf有相關的替換。 我把Liberation Sans註釋掉，加上Droid Sans。

  
        <!-- Microsoft -->
        <alias binding="same">
          <family>Arial</family>
          <accept>
            <family>Arimo</family>
            <!-- <family>Liberation Sans</family> -->
            <family>Droid Sans</family>
            <family>Albany</family>
            <family>Albany AMT</family>
          </accept>
        </alias>

  刷新緩存`fc-cache -fr`。

