---
layout: maven
pill: overview
subtitle: Maven Plugin
---
# Maven Plugin

The Flyway Open-Source Maven plugin supports **Maven 3.x** running on **Java 8** or **Java 9**. The Flyway
Enterprise Maven plugin also supports **Java 6** and **Java 7**.

## Installation

<div class="tabbable">
    <ul class="nav nav-tabs">
        <li class="active marketing-item"><a href="#tab-community" data-toggle="tab">Community Edition</a>
        </li>
        <li class="marketing-item"><a href="#tab-pro" data-toggle="tab">Pro Edition</a>
        </li>
        <li class="marketing-item"><a href="#tab-enterprise" data-toggle="tab">Enterprise Edition</a>
        </li>
    </ul>
    <div class="tab-content">
        <div class="tab-pane active" id="tab-community">
            <code>pom.xml</code>
            <pre class="prettyprint">&lt;plugin&gt;
    &lt;groupId&gt;org.flywaydb&lt;/groupId&gt;
    &lt;artifactId&gt;flyway-maven-plugin&lt;/artifactId&gt;
    &lt;version&gt;{{ site.flywayVersion }}&lt;/version&gt;
&lt;/plugin&gt;</pre>
        </div>
        <div class="tab-pane" id="tab-pro">
            <code>&lt;project-dir&gt;/pom.xml</code>
            <pre class="prettyprint">&lt;pluginRepositories&gt;
    &lt;pluginRepository&gt;
        &lt;id&gt;flyway-repo&lt;/id&gt;
        &lt;url&gt;s3://flyway-repo/release&lt;/url&gt;
    &lt;/pluginRepository&gt;
    ...
&lt;/pluginRepositories&gt;
        
&lt;build&gt;
    &lt;plugins&gt;
        &lt;plugin&gt;
            &lt;groupId&gt;org.flywaydb<strong>.pro</strong>&lt;/groupId&gt;
            &lt;artifactId&gt;flyway-maven-plugin&lt;/artifactId&gt;
            &lt;version&gt;{{ site.flywayVersion }}&lt;/version&gt;
        &lt;/plugin&gt;
    &lt;/plugins&gt;
&lt;/build&gt;</pre>
            <code>&lt;project-dir&gt;/.mvn/extensions.xml</code>
            <pre class="prettyprint">&lt;extensions&gt;
    &lt;extension&gt;
        &lt;groupId&gt;com.allogy.maven.wagon&lt;/groupId&gt;
        &lt;artifactId&gt;maven-s3-wagon&lt;/artifactId&gt;
        &lt;version&gt;1.0.1&lt;/version&gt;
    &lt;/extension&gt;
&lt;/extensions&gt;</pre>
            <code>&lt;user-home&gt;/.m2/settings.xml</code>
            <pre class="prettyprint">&lt;settings&gt;
    &lt;servers&gt;
        &lt;server&gt;
            &lt;id&gt;flyway-repo&lt;/id&gt;
            &lt;username&gt;<i>your-flyway-pro-user</i>&lt;/username&gt;
            &lt;password&gt;<i>your-flyway-pro-password</i>&lt;/password&gt;
        &lt;/server&gt;
    &lt;/servers&gt;
    ...
&lt;/settings&gt;</pre>
        </div>
        <div class="tab-pane" id="tab-enterprise">
            <code>&lt;project-dir&gt;/pom.xml</code>
            <pre class="prettyprint">&lt;pluginRepositories&gt;
    &lt;pluginRepository&gt;
        &lt;id&gt;flyway-repo&lt;/id&gt;
        &lt;url&gt;s3://flyway-repo/release&lt;/url&gt;
    &lt;/pluginRepository&gt;
    ...
&lt;/pluginRepositories&gt;
        
&lt;build&gt;
    &lt;plugins&gt;
        &lt;plugin&gt;
            &lt;groupId&gt;org.flywaydb<strong>.enterprise</strong>&lt;/groupId&gt;
            &lt;artifactId&gt;flyway-maven-plugin&lt;/artifactId&gt;
            &lt;version&gt;{{ site.flywayVersion }}&lt;/version&gt;
        &lt;/plugin&gt;
    &lt;/plugins&gt;
&lt;/build&gt;</pre>
            <code>&lt;project-dir&gt;/.mvn/extensions.xml</code>
            <pre class="prettyprint">&lt;extensions&gt;
    &lt;extension&gt;
        &lt;groupId&gt;com.allogy.maven.wagon&lt;/groupId&gt;
        &lt;artifactId&gt;maven-s3-wagon&lt;/artifactId&gt;
        &lt;version&gt;1.0.1&lt;/version&gt;
    &lt;/extension&gt;
&lt;/extensions&gt;</pre>
            <code>&lt;user-home&gt;/.m2/settings.xml</code>
            <pre class="prettyprint">&lt;settings&gt;
    &lt;servers&gt;
        &lt;server&gt;
            &lt;id&gt;flyway-repo&lt;/id&gt;
            &lt;username&gt;<i>your-flyway-enterprise-user</i>&lt;/username&gt;
            &lt;password&gt;<i>your-flyway-enterprise-password</i>&lt;/password&gt;
        &lt;/server&gt;
    &lt;/servers&gt;
    ...
&lt;/settings&gt;</pre>
        </div>
    </div>
</div>

## Goals
<table class="table table-bordered table-hover">
    <thead>
    <tr>
        <th><strong>Name</strong></th>
        <th><strong>Description</strong></th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td><a href="/documentation/maven/migrate">migrate</a></td>
        <td>Migrates the database</td>
    </tr>
    <tr>
        <td><a href="/documentation/maven/clean">clean</a></td>
        <td>Drops all objects in the configured schemas</td>
    </tr>
    <tr>
        <td><a href="/documentation/maven/info">info</a></td>
        <td>Prints the details and status information about all the migrations</td>
    </tr>
    <tr>
        <td><a href="/documentation/maven/validate">validate</a></td>
        <td>Validates the applied migrations against the ones available on the classpath</td>
    </tr>
    <tr>
        <td><a href="/documentation/maven/undo">undo</a> {% include pro.html %}</td>
        <td>Undoes the most recently applied versioned migration</td>
    </tr>
    <tr>
        <td><a href="/documentation/maven/baseline">baseline</a></td>
        <td>Baselines an existing database, excluding all migrations up to and including baselineVersion</td>
    </tr>
    <tr>
        <td><a href="/documentation/maven/repair">repair</a></td>
        <td>Repairs the schema history table</td>
    </tr>
    </tbody>
</table>

## Configuration

The Flyway Maven plugin can be configured in a wide variety of following ways, which can all be combined at will.

### Configuration section of the plugin

The easiest way is to simply use the plugin's configuration section in your `pom.xml`:

<pre class="prettyprint">&lt;plugin&gt;
    ...
    &lt;configuration&gt;
        &lt;user&gt;myUser&lt;/user&gt;
        &lt;password&gt;mySecretPwd&lt;/password&gt;
        &lt;schemas&gt;
            &lt;schema&gt;schema1&lt;/schema&gt;
            &lt;schema&gt;schema2&lt;/schema&gt;
            &lt;schema&gt;schema3&lt;/schema&gt;
        &lt;/schemas&gt;
        &lt;placeholders&gt;
            &lt;keyABC&gt;valueXYZ&lt;/keyABC&gt;
            &lt;otherplaceholder&gt;value123&lt;/otherplaceholder&gt;
        &lt;/placeholders&gt;
    &lt;/configuration&gt;
&lt;/plugin&gt;</pre>

<div class="well well-small">
    <strong>Limitation: </strong> Due to a <a href="http://mail-archives.apache.org/mod_mbox/maven-users/200708.mbox/%3C5a2cf1f60708090246l216f156esf46cc1e968b37ccd@mail.gmail.com%3E">long standing Maven bug</a>
    it is <strong>not possible to configure empty values</strong> this way. You must use one of the other configurations ways instead.
</div>

### Maven properties

To make it easy to work with Maven profiles and to logically group configuration, the Flyway Maven plugin also supports Maven properties:

<pre class="prettyprint">&lt;project&gt;
    ...
    &lt;properties&gt;
        &lt;!-- Properties are prefixed with flyway. --&gt;
        &lt;flyway.user&gt;myUser&lt;/flyway.user&gt;
        &lt;flyway.password&gt;mySecretPwd&lt;/flyway.password&gt;

        &lt;!-- List are defined as comma-separated values --&gt;
        &lt;flyway.schemas&gt;schema1,schema2,schema3&lt;/flyway.schemas&gt;

        &lt;!-- Individual placeholders are prefixed by flyway.placeholders. --&gt;
        &lt;flyway.placeholders.keyABC&gt;valueXYZ&lt;/flyway.placeholders.keyABC&gt;
        &lt;flyway.placeholders.otherplaceholder&gt;value123&lt;/flyway.placeholders.otherplaceholder&gt;
    &lt;/properties&gt;
    ...
&lt;/project&gt;</pre>

### settings.xml

For storing the database user and password, Maven `settings.xml` files can also be used:</p>

<pre class="prettyprint">&lt;settings&gt;
    &lt;servers&gt;
        &lt;server&gt;
            &lt;!-- By default Flyway will look for the server with the id 'flyway-db' --&gt;
            &lt;!-- This can be customized by configuring the 'serverId' property --&gt;
            &lt;id&gt;flyway-db&lt;/id&gt;
            &lt;username&gt;myUser&lt;/username&gt;
            &lt;password&gt;mySecretPwd&lt;/password&gt;
        &lt;/server&gt;
    &lt;/servers&gt;
&lt;/settings&gt;</pre>

Both regular and encrypted settings files are supported.

### Environment Variables

To make it ease to work with cloud and containerized environments, Flyway also supports configuration via
[environment variables](/documentation/envvars). Check out the [Flyway environment variable reference](/documentation/envvars) for details.

### System properties

Configuration can also be supplied directly via the command-line using JVM system properties:

<pre class="console"><span>&gt;</span> mvn -Dflyway.user=myUser -Dflyway.schemas=schema1,schema2 -Dflyway.placeholders.keyABC=valueXYZ</pre>

### Config files

[Config files](/documentation/configfiles) are supported by the Flyway Maven plugin. If you are not familiar with them,
check out the [Flyway config file structure and settings reference](/documentation/configfiles) first.

Flyway will search for and automatically load the `<user-home>/flyway.conf` config file if present.

It is also possible to point Flyway at one or more additional config files. This is achieved by
supplying the System property `flyway.configFiles` as follows:

<pre class="console"><span>&gt;</span> mvn <strong>-Dflyway.configFiles=</strong>path/to/myAlternativeConfig.conf flyway:migrate</pre>

To pass in multiple files, separate their names with commas:

<pre class="console"><span>&gt;</span> mvn <strong>-Dflyway.configFiles</strong>=path/to/myAlternativeConfig.conf,other.conf flyway:migrate</pre>

Relative paths are relative to the directory containing your `pom.xml` file. 

Alternatively you can also use the `FLYWAY_CONFIG_FILES` environment variable for this.
When set it will take preference over the command-line parameter.

<pre class="console"><span>&gt;</span> export <strong>FLYWAY_CONFIG_FILES</strong>=path/to/myAlternativeConfig.conf,other.conf</pre>

By default Flyway loads configuration files using UTF-8. To use an alternative encoding, pass the system property <code>flyway.configFileEncoding</code>
    as follows:
<pre class="console"><span>&gt;</span> mvn <strong>-Dflyway.configFileEncoding=</strong>ISO-8859-1 flyway:migrate</pre>

This is also possible via the configuration section of the plugin or Maven properties, as described above.

Alternatively you can also use the `FLYWAY_CONFIG_FILE_ENCODING` environment variable for this.
    When set it will take preference over the command-line parameter.

<pre class="console"><span>&gt;</span> export <strong>FLYWAY_CONFIG_FILE_ENCODING</strong>=ISO-8859-1</pre>

### Overriding order

The Flyway Maven plugin has been carefully designed to load and override configuration in a sensible order.

Settings are loaded in the following order (higher items in the list take precedence over lower ones):
1. System properties
2. Environment variables
3. Custom config files
4. Maven properties
5. Plugin configuration section 
6. Credentials from `settings.xml` 
7. `<user-home>/flyway.conf`
8. Flyway Maven plugin defaults

The means that if for example `flyway.url` is both present in a config file and passed as `-Dflyway.url=` from the command-line,
the JVM system property passed in via the command-line will take precedence and be used.  

<p class="next-steps">
    <a class="btn btn-primary" href="/documentation/maven/migrate">Maven: migrate <i class="fa fa-arrow-right"></i></a>
</p>
