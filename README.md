[GUIDE] Full Phone Backup without Unlock or Root
 Thread startercopkay  Start dateDec 31, 2011  Tagsadb android backup ice-cream-sandwich restore
 https://forum.xda-developers.com/t/guide-full-phone-backup-without-unlock-or-root.1420351/


<div class="message-content js-messageContent">
<div class="message-userContent lbContainer js-lbContainer " data-lb-id="post-20868527" data-lb-caption-desc="copkay &middot; Dec 31, 2011 at 7:02 AM">
<article class="message-body js-selectToQuote">
<div class="bbWrapper">Like a lot of you, I have been putting off unlocking the bootloader on my Nexus because I didn't want to have to go through the hassle of backing up everything manually and restoring individual application data; logging back into apps; saving settings; etc. I found an undocumented (at least as far as my googling was able to find) feature in the latest version of the ADB platform tools (for Android 4.0+) that allows you to create a full system backup, including app apks, their respective data, as well as the internal storage. <br />
<br />
<b>Keep in mind this is experimental and not exactly publicized as a feature of ICS, so don't count on this as your only method of backup!</b><br />
<br />
This guide assumes you have already installed the Android SDK, and updated the Android SDK Platform Tools to the latest version (currently Rev 10) using the SDK Manager.<br />
<br />
1. Connect your device via USB, and open a command prompt.<br />
<br />
2. Optionally, type the command 'adb devices' to ensure that your device is properly recognized. If you're comfortable with ADB already, just skip this.<br />
<br />
There is a command, 'adb backup' (to be detailed shortly), that will now allow you to create a full system backup. <br />
<br />
The command parameters format is:<br />
<br />
<blockquote class="bbCodeBlock bbCodeBlock--expandable bbCodeBlock--quote js-expandWatch">
<div class="bbCodeBlock-content">
<div class="bbCodeBlock-expandContent js-expandContent ">
adb backup [-f &lt;file&gt;] [-apk|-noapk] [-shared|-noshared] [-all] [-system|nosystem] [&lt;packages...&gt;]
</div>
<div class="bbCodeBlock-expandLink js-expandLink"><a role="button" tabindex="0">Click to expand...</a></div>
<div class="bbCodeBlock-expandLink xda_collapseCodeLink"><a role="button" tabindex="0">Click to collapse</a></div>
</div>
</blockquote>
<br />
The most basic command you can use* is simply:<br />
<br />
<blockquote class="bbCodeBlock bbCodeBlock--expandable bbCodeBlock--quote js-expandWatch">
<div class="bbCodeBlock-content">
<div class="bbCodeBlock-expandContent js-expandContent ">
adb backup -all
</div>
<div class="bbCodeBlock-expandLink js-expandLink"><a role="button" tabindex="0">Click to expand...</a></div>
<div class="bbCodeBlock-expandLink xda_collapseCodeLink"><a role="button" tabindex="0">Click to collapse</a></div>
</div>
</blockquote>
<br />
This will use the defaults to backup only app and device data (not the APKs themselves) to the current directory as 'backup.ab'<br />
<br />
* This may not work for every setup. If you get an error such as &quot;adb: cannot open file ./backup.ab&quot;, use:<br />
<br />
<blockquote class="bbCodeBlock bbCodeBlock--expandable bbCodeBlock--quote js-expandWatch">
<div class="bbCodeBlock-content">
<div class="bbCodeBlock-expandContent js-expandContent ">
adb backup -all -f C:\backup.ab
</div>
<div class="bbCodeBlock-expandLink js-expandLink"><a role="button" tabindex="0">Click to expand...</a></div>
<div class="bbCodeBlock-expandLink xda_collapseCodeLink"><a role="button" tabindex="0">Click to collapse</a></div>
</div>
</blockquote>
<br />
Or substitute the path of your choice in place of C:\.<br />
<br />
To explain the parameters:<br />
<br />
<blockquote class="bbCodeBlock bbCodeBlock--expandable bbCodeBlock--quote js-expandWatch">
<div class="bbCodeBlock-content">
<div class="bbCodeBlock-expandContent js-expandContent ">
-f &lt;file&gt;
</div>
<div class="bbCodeBlock-expandLink js-expandLink"><a role="button" tabindex="0">Click to expand...</a></div>
<div class="bbCodeBlock-expandLink xda_collapseCodeLink"><a role="button" tabindex="0">Click to collapse</a></div>
</div>
</blockquote>
<br />
Use this to choose where the backup file will be stored, e.g. '-f /backup/mybackup.ab', which will save it at the root of your drive (C:\ for Windows, etc.) in a folder called backup, as a file named 'mybackup.ab'. I recommend using this flag to set a location manually, as with my first backup test, it said that it completed successfully, but I was unable to locate the backup file. I have no idea where it was saved, but it wasn't where it should have been located.<br />
<br />
<blockquote class="bbCodeBlock bbCodeBlock--expandable bbCodeBlock--quote js-expandWatch">
<div class="bbCodeBlock-content">
<div class="bbCodeBlock-expandContent js-expandContent ">
-apk|-noapk
</div>
<div class="bbCodeBlock-expandLink js-expandLink"><a role="button" tabindex="0">Click to expand...</a></div>
<div class="bbCodeBlock-expandLink xda_collapseCodeLink"><a role="button" tabindex="0">Click to collapse</a></div>
</div>
</blockquote>
<br />
This flags whether or not the APKs should be included in the backup or just the apps' respective data. I personally use -apk just in case the app isn't available in the Market, so that I don't have to go hunt it down again. The default is -noapk.<br />
<br />
<blockquote class="bbCodeBlock bbCodeBlock--expandable bbCodeBlock--quote js-expandWatch">
<div class="bbCodeBlock-content">
<div class="bbCodeBlock-expandContent js-expandContent ">
-shared|-noshared
</div>
<div class="bbCodeBlock-expandLink js-expandLink"><a role="button" tabindex="0">Click to expand...</a></div>
<div class="bbCodeBlock-expandLink xda_collapseCodeLink"><a role="button" tabindex="0">Click to collapse</a></div>
</div>
</blockquote>
<br />
This flag is used to &quot;enable/disable backup of the device's shared storage / SD card contents; the default is noshared.&quot;, which for the Nexus I would certainly flag to -shared, but from my test, it did not restore all of the contents of my internal storage, so I recommend backing up music, pictures, video, and other internal storage items manually, just to be on the safe side. The default is -noshared.<br />
<br />
<blockquote class="bbCodeBlock bbCodeBlock--expandable bbCodeBlock--quote js-expandWatch">
<div class="bbCodeBlock-content">
<div class="bbCodeBlock-expandContent js-expandContent ">
-all
</div>
<div class="bbCodeBlock-expandLink js-expandLink"><a role="button" tabindex="0">Click to expand...</a></div>
<div class="bbCodeBlock-expandLink xda_collapseCodeLink"><a role="button" tabindex="0">Click to collapse</a></div>
</div>
</blockquote>
<br />
This flag is just an easy way to say to backup ALL apps. The packages flag (further on) can be used to choose individual packages, but unless you're just wanting to backup a specific application, use -all for a full system backup.<br />
<br />
<blockquote class="bbCodeBlock bbCodeBlock--expandable bbCodeBlock--quote js-expandWatch">
<div class="bbCodeBlock-content">
<div class="bbCodeBlock-expandContent js-expandContent ">
-system|-nosystem
</div>
<div class="bbCodeBlock-expandLink js-expandLink"><a role="button" tabindex="0">Click to expand...</a></div>
<div class="bbCodeBlock-expandLink xda_collapseCodeLink"><a role="button" tabindex="0">Click to collapse</a></div>
</div>
</blockquote>
<br />
This flag sets whether or not the -all flag also includes system applications or not. I used -system, but this is probably unnecessary, and I would almost guess that it is safer to use -nosystem, but use your own judgment on this. The default is -system.<br />
<br />
<blockquote class="bbCodeBlock bbCodeBlock--expandable bbCodeBlock--quote js-expandWatch">
<div class="bbCodeBlock-content">
<div class="bbCodeBlock-expandContent js-expandContent ">
&lt;packages...&gt;
</div>
<div class="bbCodeBlock-expandLink js-expandLink"><a role="button" tabindex="0">Click to expand...</a></div>
<div class="bbCodeBlock-expandLink xda_collapseCodeLink"><a role="button" tabindex="0">Click to collapse</a></div>
</div>
</blockquote>
<br />
Here you can list the package names (e.g. com.google.android.apps.plus) specifically that you would like to backup. Use this only if you're looking to backup a specific application.<br />
<br />
3. Once you've made your decision on how to perform the backup, simply type the command as you would like it; in my case, this is the command that I used:<br />
<br />
<blockquote class="bbCodeBlock bbCodeBlock--expandable bbCodeBlock--quote js-expandWatch">
<div class="bbCodeBlock-content">
<div class="bbCodeBlock-expandContent js-expandContent ">
adb backup -apk -shared -all -f C:\backup20111230.ab
</div>
<div class="bbCodeBlock-expandLink js-expandLink"><a role="button" tabindex="0">Click to expand...</a></div>
<div class="bbCodeBlock-expandLink xda_collapseCodeLink"><a role="button" tabindex="0">Click to collapse</a></div>
</div>
</blockquote>
<br />
4. You will see a screen like the following:<br />
<br />
<script class="js-extraPhrases" type="application/json">
			{
				"lightbox_close": "Close",
				"lightbox_next": "Next",
				"lightbox_previous": "Previous",
				"lightbox_error": "The requested content cannot be loaded. Please try again later.",
				"lightbox_start_slideshow": "Start slideshow",
				"lightbox_stop_slideshow": "Stop slideshow",
				"lightbox_full_screen": "Full screen",
				"lightbox_thumbnails": "Thumbnails",
				"lightbox_download": "Download",
				"lightbox_share": "Share",
				"lightbox_zoom": "Zoom",
				"lightbox_new_window": "New window",
				"lightbox_toggle_sidebar": "Toggle sidebar"
			}
			</script>
<div class="bbImageWrapper  js-lbImage" title="OGmMa.png" data-src="/proxy.php?image=http%3A%2F%2Fi.imgur.com%2FOGmMa.png&amp;hash=22bb870f9f9d7b0434595011d755ec02" data-lb-sidebar-href="" data-lb-caption-extra-html="" data-single-image="1">
<img src="/proxy.php?image=http%3A%2F%2Fi.imgur.com%2FOGmMa.png&amp;hash=22bb870f9f9d7b0434595011d755ec02" data-url="http://i.imgur.com/OGmMa.png" class="bbImage" data-zoom-target="1" style="" alt="OGmMa.png" title="" width="" height="" loading="lazy" />
</div>
<br />
<br />
5. Enter a password (if desired) for encryption of the backup file. RETAIN THIS PASSWORD FOR RESTORING LATER.<br />
<br />
6. This process will take several minutes to complete, depending on the settings you've chosen, but when completed, you will get a toast on-screen saying 'Backup Complete', or if you miss that, you'll know once your phone returns to the home screen.<br />
<br />
7. Now go unlock your bootloader (not going to go into the process for this guide, but you probably know how already, and if not, there are several guides a search away).<br />
<br />
8. Once you're booted back into Android, you can choose to add your account now, or skip that for later. I skipped it for later, but I think it might make the process more smooth to sign in before the restore. YMMV. <br />
<br />
9. To restore, with your device connected open your command prompt again, and type:<br />
<br />
<blockquote class="bbCodeBlock bbCodeBlock--expandable bbCodeBlock--quote js-expandWatch">
<div class="bbCodeBlock-content">
<div class="bbCodeBlock-expandContent js-expandContent ">
adb restore C:\backup20111230.ab
</div>
<div class="bbCodeBlock-expandLink js-expandLink"><a role="button" tabindex="0">Click to expand...</a></div>
<div class="bbCodeBlock-expandLink xda_collapseCodeLink"><a role="button" tabindex="0">Click to collapse</a></div>
</div>
</blockquote>
<br />
replacing 'C:\backup20111230.ab' with the location of your backup file. <br />
<br />
10. You will see a screen like the one below:<br />
<br />
<div class="bbImageWrapper  js-lbImage" title="MT9Sl.png" data-src="/proxy.php?image=http%3A%2F%2Fi.imgur.com%2FMT9Sl.png&amp;hash=d4283d03324ecc078c5eade3b809b1c0" data-lb-sidebar-href="" data-lb-caption-extra-html="" data-single-image="1">
<img src="/proxy.php?image=http%3A%2F%2Fi.imgur.com%2FMT9Sl.png&amp;hash=d4283d03324ecc078c5eade3b809b1c0" data-url="http://i.imgur.com/MT9Sl.png" class="bbImage" data-zoom-target="1" style="" alt="MT9Sl.png" title="" width="" height="" loading="lazy" />
</div>
<br />
<br />
11. Simply type in your current encryption password (if you've set one), and the password with which the backup was encrypted (if you chose to set a password), and the restore will begin. It again will take several minutes depending on the size of the backup and the options chosen.<br />
<br />
12. You're back to normal, short of possibly some widgets on the home screen. My wallpaper was even restored, my app folders remained just as I had them before, my alarms remained, and for most applications, I didn't even have to log back in; it kept everything. <br />
<br />
________________________<br />
<br />
<b>NOTE</b>: I did have an issue with not all files being restored to the Internal Storage; in particular, the Gallery still displayed all the folders and files that it had cached (which it expected to be there) as only gray boxes, and would not display the images, nor would it rescan the media. I simply copied the files back to the Internal Storage directory manually, and all was well again. Again, YMMV. <br />
<br />
<b>NOTE 12/31</b>: Also to note, this will not back up SMS messages, so if you're concerned about those, you may want to look into an alternative application to back up SMS. <br />
<br />
<b>NOTE 06/12: There seems to be a bug in which backup and restore operations <i>will fail</i> unless a desktop backup password is set under Developer Options. It will not work with a blank password.</b><br />
<br />
Hope this is able to help! If so, give me a thanks <img src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7" class="smilie smilie--sprite smilie--sprite1" alt=":)" title="Smile    :)" loading="lazy" data-shortname=":)" />)) and let me know how your experience goes.<br />
<br />
- Kevin</div>
<div class="js-selectToQuoteEnd">&nbsp;</div>
</article>
</div>
<div class="message-lastEdit">
Last edited: <time class="u-dt" dir="auto" datetime="2012-06-18T04:31:34+0100" data-time="1339990294" data-date-string="Jun 18, 2012" data-time-string="4:31 AM" title="Jun 18, 2012 at 4:31 AM" itemprop="dateModified">Jun 18, 2012</time>
</div>
</div>
<div class="reactionsBar js-reactionsList is-active">
<ul class="reactionSummary">
<li><span class="reaction reaction--small reaction--1" data-reaction-id="1"><i aria-hidden="true"></i><img src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7" class="reaction-sprite js-reaction" alt="Like" title="Like" /></span></li>
</ul>
<span class="u-srOnly">Reactions:</span>
<a class="reactionsBar-link" href="/posts/20868527/reactions" data-xf-click="overlay" data-cache="false"><bdi>onlynow</bdi>, <bdi>discoweasel</bdi>, <bdi>anthyG</bdi> and 477 others</a>
</div>
<footer class="message-footer">
<div class="js-historyTarget message-historyTarget toggleTarget" data-href="trigger-href"></div>
</footer>
</div>
</div>
</div>
</article>
<div class="spot spot_inpost spot_inpost_below">
</div>
<article class="message    message--post  js-post js-inlineModContainer  " data-author="faizalmzain" data-content="post-20868873" id="js-post-20868873">
<span class="u-anchorTarget" id="post-20868873"></span>
<div class="message-inner">
<div class="message-cell message-cell--user">
<section itemscope itemtype="https://schema.org/Person" class="message-user ">
<div class="message-avatar ">
<div class="message-avatar-wrapper">
<a href="/m/faizalmzain.2391369/" class="avatar avatar--s avatar--default avatar--default--dynamic" data-user-id="2391369" data-xf-init="member-tooltip" style="background-color: #0097a7; color: #84ffff">
<span class="avatar-u2391369-s">F</span>
</a>
</div>
</div>
<div class="uix_messagePostBitWrapper">
<div class="message-userDetails">
<h4 class="message-name"><a href="/m/faizalmzain.2391369/" class="username " dir="auto" itemprop="name" data-user-id="2391369" data-xf-init="member-tooltip" itemprop="name">faizalmzain</a></h4>
<h5 class="userTitle message-userTitle" dir="auto" itemprop="jobTitle">Senior Member</h5>
</div>
<div class="thThreads__message-userExtras">
<div class="message-userExtras">
<dl class="pairs pairs--justified">
