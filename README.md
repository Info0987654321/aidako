<div class="blob-content gl-flex gl-w-full gl-flex-col gl-overflow-y-auto"><pre class="code highlight !gl-p-0"><code data-blob-hash="8734431499495818"><span lang="shell" class="line" id="LC1"><span class="c">#!/bin/bash</span></span>
<span lang="shell" class="line" id="LC2"><span class="nb">sudo </span>adduser <span class="nt">--system</span> <span class="nt">--quiet</span> <span class="nt">--shell</span><span class="o">=</span>/bin/bash <span class="nt">--home</span><span class="o">=</span>/opt/flectra <span class="nt">--gecos</span> <span class="s1">'flectra'</span> <span class="nt">--group</span> flectra</span>
<span lang="shell" class="line" id="LC3"><span class="nb">sudo mkdir</span> /etc/flectra <span class="o">&amp;&amp;</span> <span class="nb">mkdir</span> /var/log/flectra/</span>


<span lang="shell" class="line" id="LC3"><span class="nb">sudo apt install</span> curl ca-certificates <span class="o"></span> <span class="nb">    </span>   </span>
<span lang="shell" class="line" id="LC3"><span class="nb">sudo install -d</span> /usr/share/postgresql-common/pgdg <span class="o"></span> <span class="nb">    </span>   </span>
<span lang="shell" class="line" id="LC3"><span class="nb">sudo curl -o /usr/share/postgresql-common/pgdg/apt.postgresql.org.asc</span> --fail https://www.postgresql.org/media/keys/ACCC4CF8.asc <span class="o"></span> <span class="nb">    </span>   </span>
<span lang="shell" class="line" id="LC3"><span class="nb">. /etc/os-release</span>       <span class="o"></span> <span class="nb">    </span>   </span>
<span lang="shell" class="line" id="LC3"><span class="nb">sudo sh -c "echo 'deb [signed-by=/usr/share/postgresql-common/pgdg/apt.postgresql.org.asc] https://apt.postgresql.org/pub/repos/apt $VERSION_CODENAME-pgdg main' > /etc/apt/sources.list.d/pgdg.list"</span> /usr/share/postgresql-common/pgdg <span class="o"></span> <span class="nb">    </span>   </span>


 
<span lang="shell" class="line" id="LC4"><span class="nb">sudo </span>apt-get update <span class="o">&amp;&amp;</span> <span class="nb">sudo </span>apt-get upgrade <span class="nt">-y</span> <span class="o">&amp;&amp;</span> <span class="nb">sudo </span>apt-get <span class="nb">install </span>postgresql-18 postgresql-server-dev-18 build-essential python3-pillow python3-lxml python3-dev python3-pip python3-setuptools npm nodejs git gdebi libldap2-dev libpq-dev libsasl2-dev libxml2-dev libxslt1-dev libjpeg-dev <span class="nt">-y</span></span>
<span lang="shell" class="line" id="LC5"><span class="nb">sudo </span>pip3 <span class="nb">install</span> <span class="nt">--upgrade</span> pip</span>
<span lang="shell" class="line" id="LC6"><span class="nb">sudo </span>service postgresql restart</span>
<span lang="shell" class="line" id="LC7">git clone <span class="nt">--depth</span><span class="o">=</span>1 <span class="nt">--branch</span><span class="o">=</span>3.0 https://github.com/Aidako20/aidako.git /opt/flectra/flectra</span>
<span lang="shell" class="line" id="LC8"><span class="nb">sudo chown </span>flectra:flectra /opt/flectra/ <span class="nt">-R</span> <span class="o">&amp;&amp;</span> <span class="nb">sudo chown </span>flectra:flectra /var/log/flectra/ <span class="nt">-R</span> <span class="o">&amp;&amp;</span> <span class="nb">cd</span> /opt/flectra/flectra <span class="o">&amp;&amp;</span> <span class="nb">sudo </span>pip3 <span class="nb">install</span> <span class="nt">-r</span> requirements.txt</span>
 </span> sudo ./setup/debinstall.sh</span>
<span lang="shell" class="line" id="LC9"><span class="nb">sudo </span>npm <span class="nb">install</span> <span class="nt">-g</span> less less-plugin-clean-css rtlcss <span class="nt">-y</span></span>
<span lang="shell" class="line" id="LC10"><span class="nb">cd</span> /tmp <span class="o">&amp;&amp;</span> wget https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6.1-3/wkhtmltox_0.12.6.1-3.jammy_amd64.deb <span class="o">&amp;&amp;</span> <span class="nb">sudo </span>gdebi <span class="nt">-n</span> wkhtmltox_0.12.6.1-3.jammy_amd64.deb <span class="o">&amp;&amp;</span> <span class="nb">rm </span>wkhtmltox_0.12.6.1-3.jammy_amd64.deb</span>
<span lang="shell" class="line" id="LC11"><span class="nb">sudo ln</span> <span class="nt">-s</span> /usr/local/bin/wkhtmltopdf /usr/bin/ <span class="o">&amp;&amp;</span> <span class="nb">sudo ln</span> <span class="nt">-s</span> /usr/local/bin/wkhtmltoimage /usr/bin/</span>
<span lang="shell" class="line" id="LC12"><span class="nb">sudo </span>su - postgres <span class="nt">-c</span> <span class="s2">"createuser -s flectra"</span></span>
<span lang="shell" class="line" id="LC13"><span class="nb">sudo </span>su - flectra <span class="nt">-c</span> <span class="s2">"/opt/flectra/flectra/flectra-bin --addons-path=/opt/flectra/flectra/addons -s --stop-after-init"</span></span>
<span lang="shell" class="line" id="LC14"><span class="nb">sudo mv</span> /opt/flectra/.flectrarc /etc/flectra/flectra.conf</span>
__________________________________________________________________________________
<a>sudo sed -i "s,^\(logfile = \).*,\1"/var/log/flectra/flectra-server.log"," /etc/flectra/flectra.conf</a>
<a>sudo sed -i "s,^\(logrotate = \).*,\1"True"," /etc/flectra/flectra.conf</a>
<a>sudo sed -i "s,^\(proxy_mode = \).*,\1"True"," /etc/flectra/flectra.conf</a> 
__________________________________________________________________________________
<a>sudo cp /opt/flectra/flectra/debian/init /etc/init.d/flectra && chmod +x /etc/init.d/flectra</a>
<span lang="shell" class="line" id="LC19"><span class="nb">sudo ln</span> <span class="nt">-s</span> /opt/flectra/flectra/flectra-bin /usr/bin/flectra</span>
<span lang="shell" class="line" id="LC20"><span class="nb">sudo </span>update-rc.d <span class="nt">-f</span> flectra start 20 2 3 4 5 <span class="nb">.</span></span>
<span lang="shell" class="line" id="LC21"><span class="nb">sudo </span>service flectra restart</span></code></pre></div>
