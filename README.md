# dell-dsucreateiso
# Dell utilities

<!DOCTYPE html>
<html ng-app='myApp'>
<head>
    <title>Dell System Update</title>

    <meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=no">
    <meta name="apple-mobile-web-app-capable" content="yes" />
    <meta name="mobile-web-app-capable" content="yes">

    <script src='./js/cui-vendor.min.js'></script>
    <script src='./js/cui.min.js'></script>

    <link rel="stylesheet" href="./css/cui.min.css">
    <script>
        angular.module('myApp', ['cui']).
        controller('AppController', function ($scope, cuiAboutBox) {

            $scope.showAboutBox = function () {
                var aboutBox = cuiAboutBox({
                    applicationName: 'Dell System Update',
                    tabs: [{
                        label: 'About',
                        active: true,
                        template: 'aboutBox.about'
                    }]
                });

                aboutBox.modal.show();
                $scope.showAboutBox = aboutBox.modal.show;
            }
        });
    </script>

</head>
<body ng-controller='AppController'>
    <!--[if IE]>
    <style>
    #nav {
        list-style: none;
        font-weight: bold;
        margin-bottom: 10px;
        width: 100%;
        text-align: center;
        background-color: #282828;
        height:74px;
    }
    </style>
    <div id='nav'>
    <img src='css/image/dsu.jpg'/ align=left>
    </div>
    <br>
    <![endif]-->


    <cui-application-frame application-name='Dell System Update' navigation-items='applicationframe.navigation' masthead-show-controls=true>

        <div cui-content>
            <!-- Page Content -->
			
			<br>
            <h1> Dell System Update (DSU) </h1>
            
            Starting with DSU 1.7 information on DSU is located at the following link:
            <ul>
                <li><a href="https://www.dell.com/support/kbdoc/en-us/000130590/dell-emc-system-update-dsu">Dell technical resource</a></li>
				<li>Note: Starting with DSU 1.7, consent is required prior to installing public keys on target systems.</li>
            </ul>
			
			<h1> Repository setup </h1>
			ChangeLog from previous repository: <a href="changelog.html">Here</a><p>
			To configure the repository, use the following commands:<br>
			<i>1. curl -O https://linux.dell.com/repo/hardware/dsu/bootstrap.cgi</i><br>
			<i>2. bash bootstrap.cgi</i><br>
			<font color="red">Note: Consent is required prior to installing public keys on target systems.</font>
			
			<h1> DSU 1.8 Known Issue on RHEL 8.x OS</h1>
			<p><font ><b>Error:</b> dsu: error while loading shared libraries: libssh2.so.1: cannot open shared object file: No such file or directory</font></p>
			<p><font ><b>Workaround:</b> ln -s $(find /usr/lib64 -name libssh* -type f) /usr/lib64/libssh2.so.1 </font></p>
			
			<li>Note: The workaround enables DSU to run on the same host. To enable remote functionality libssh2 has to be installed.
				This dependency addressed in DSU 1.9</li>
			
			<h1> Install DSU</h1>
			To install DSU using the repository, use the following command<br>
			<i><p>#yum install dell-system-update</p></i>
			
            
			<h1>Install OMSA</h1>
            To install OMSA using this repository, use the following commands:<br>
            <h3><i>Red Hat Enterprise Linux Servers</i></h3>
            <i><p>#yum install srvadmin-all</p></i>
			<ul>
			<li>
				<i><p><b><font color="red"> Please re-run repository setup commands to import the updated signature keys </font></b></p></i>
			</li>
			</ul>
            <h3><i>SUSE Linux Enterprise Servers</i></h3>
            <i><p>#zypper install srvadmin-all</p></i>
            OMSA services should be manually started after installing/upgrading OMSA using DSU repository

            <a name="omsa_upgrade"><h1>Upgrade OMSA</h1></a>
            To upgrade OMSA using this repository, where an OMSA version is already installed in the system, use the following commands.<br>
            <h3><i>Red Hat Enterprise Linux Servers</i></h3>
            <i><p>#yum --disablerepo=* --enablerepo=dell-system-update_dependent upgrade</p></i>
            <h3><i>SUSE Linux Enterprise Servers</i></h3>
            <i><p>#zypper mr -da;  zypper mr  -e "dell-system-update_dependent" ; zypper  update;  zypper mr -ea;</p></i>
            Note:-To update from local repository (custom), use the OMSA repository name instead of dell-system-update_dependent in the commands. <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;In case of zypper upgrade, if there are repositories disabled by you, this command sequence will enable the repositories. You have to disable the repositories again manually.
            		
				
			<h1>Other supporting documents and links</h1>
            In addition to this guide, you can access the following guides available at dell.com/support/manuals.<br>
            <ul>
                <li>Dell Systems Management - OpenManage Software Support Matrix</li>
                <li>Dell OpenManage Server Administrator Installation Guide</li>
                <li>Dell OpenManage Server Administrator User's Guide</li>
                <li>Previous Dell Linux Repository : <a href='https://linux.dell.com/repo/hardware/'>Click Here</a></li>
                <li>Supported Platforms : <b>  <a href='http://linux.dell.com/repo/hardware/dsu/platforms.html'>Click Here</a> </b></li>
				<ul>
					<li><b>Note: DSU Ubuntu enablement is only available for 12G and 13G systems</b></li>
				</ul>
                <li>Sample Kickstart Files : <a href='https://linux.dell.com/repo/hardware/sampleks/'>Click Here</a></li>
		<li>ISO Generator Script : <a href='https://linux.dell.com/repo/hardware/scripts/'>Click Here</a></li>
            </ul>
            <p>
                To get the complete list of options of DSU (On Microsoft Windows and Linux), use <i> #dsu --help </i>
            <p>
                <h1>Support</h1>
            <p>A good place for support for this repository is the <a href='https://lists.us.dell.com/mailman/listinfo/linux-poweredge'>linux-poweredge</a> mailing list.</p>
            <br>
            <h1>File list</h1>
            <p>Use the following links to browse the contents of the repository</p>
            <a href="./os_independent"><img src="https://linux.dell.com/icons/folder.gif"> OS independent</img></a><br>
            <a href="./os_dependent"><img src="https://linux.dell.com/icons/folder.gif"> OS dependent</img></a><br>
            <p>
                <br>
                <!-- Page Content ends -->
        </div>
        <!-- Page Content ends -->
    </cui-application-frame>
    <script>
        (function (i, s, o, g, r, a, m) {
            i['GoogleAnalyticsObject'] = r; i[r] = i[r] || function () {
                (i[r].q = i[r].q || []).push(arguments)
            }, i[r].l = 1 * new Date(); a = s.createElement(o),
            m = s.getElementsByTagName(o)[0]; a.async = 1; a.src = g; m.parentNode.insertBefore(a, m)
        })(window, document, 'script', '//www.google-analytics.com/analytics.js', 'ga');

        ga('create', 'UA-52996950-4', 'auto');
        ga('send', 'pageview');

    </script>
</body>
</html>
