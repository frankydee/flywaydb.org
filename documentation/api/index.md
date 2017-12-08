---
layout: api
pill: overview
subtitle: API
---
# API

Flyway brings the largest benefits when **integrated within an application**. By integrating Flyway
you can ensure that the application and its **database will always be compatible**, with no manual
intervention required. Flyway checks the version of the database and applies new migrations automatically
**before** the rest of the application starts. This is important, because the database must first
be migrated to a state the rest of the code can work with.

## Supported Java Versions

- `Java 9`
- `Java 8`
- `Java 7` {% include enterprise.html %}
- `Java 6` {% include enterprise.html %}

## Download

<table class="table">
    <thead>
    <tr>
        <th><strong>Binary</strong></th>
        <th><strong>Source</strong></th>
    </tr>
    </thead>
    <tr>
        <td>
            <a href="http://repo1.maven.org/maven2/org/flywaydb/flyway-core/{{site.flywayVersion}}/flyway-core-{{site.flywayVersion}}.jar">flyway-core-{{site.flywayVersion}}.jar</a>
        </td>
        <td>
            <a href="http://repo1.maven.org/maven2/org/flywaydb/flyway-core/{{site.flywayVersion}}/flyway-core-{{site.flywayVersion}}-sources.jar">flyway-core-{{site.flywayVersion}}-sources.jar</a>
        </td>
    </tr>
</table>

<h3>Build Tools</h3>
<div class="tabbable">
    <ul class="nav nav-tabs">
        <li class="active marketing-item"><a href="#tab-maven" data-toggle="tab"><i class="fa fa-maxcdn"></i> Maven</a>
        </li>
        <li class="marketing-item"><a href="#tab-gradle" data-toggle="tab"><i class="fa fa-cogs"></i> Gradle</a>
        </li>
        <li class="marketing-item"><a href="#tab-ant" data-toggle="tab"><i class="fa fa-wrench"></i> Ant + Ivy</a>
        </li>
        <li class="marketing-item"><a href="#tab-sbt" data-toggle="tab"><i class="fa fa-angle-right"></i> SBT</a>
        </li>
    </ul>
    <div class="tab-content">
        <div class="tab-pane active" id="tab-maven">
            <pre class="prettyprint">&lt;dependency&gt;
    &lt;groupId&gt;org.flywaydb&lt;/groupId&gt;
    &lt;artifactId&gt;flyway-core&lt;/artifactId&gt;
    &lt;version&gt;{{ site.flywayVersion }}&lt;/version&gt;
&lt;/dependency&gt;</pre>
        </div>
        <div class="tab-pane" id="tab-gradle">
            <pre class="prettyprint">compile "org.flywaydb:flyway-core:{{ site.flywayVersion }}"</pre>
        </div>
        <div class="tab-pane" id="tab-ant">
            <pre class="prettyprint">&lt;dependency org="org.flywaydb" name="flyway-core" rev="{{ site.flywayVersion }}"/&gt;</pre>
        </div>
        <div class="tab-pane" id="tab-sbt">
            <pre class="prettyprint">"org.flywaydb" % "flyway-core" % "{{ site.flywayVersion }}"</pre>
        </div>
    </div>
</div>

<h2>The Flyway Class</h2>

<p>The central piece of Flyway&#x27;s database migration infrastructure is the <strong><a
        href="/documentation/api/javadoc/org/flywaydb/core/Flyway">org.flywaydb.core.Flyway</a></strong>
    class. It is your <strong>one-stop shop</strong> for working with Flyway programmatically. It serves both as a
    <strong>configuration</strong> and a <strong>launching</strong> point for all of Flyway&#x27;s functions. </p>

<h2>Programmatic Configuration (Java)</h2>

<p>Flyway is super easy to use programmatically: </p><pre class="prettyprint">import org.flywaydb.core.Flyway;

...
Flyway flyway = new Flyway();
flyway.setDataSource(...);
flyway.migrate();

// Start the rest of the application (incl. Hibernate)
...</pre>

<div class="well"><strong>Tip:</strong> When running inside a <a href="https://boxfuse.com">Boxfuse</a>
    instance (both locally and on AWS), Flyway will automatically use the JDBC url, user and password
    <a href="https://boxfuse.com/docs/databases#envvars">provided by Boxfuse</a>.</div>

<h2>Programmatic Configuration (Android)</h2>

<p>In order to use Flyway on Android you have to add flyway-core as well as SQLDroid as dependencies. There are two things to keep in mind with Android: First, you have to load the migrations as <i>assets</i>, not <i>resources</i> and second, you have to let Flyway know your Android context, by calling <code>ContextHolder.setContext</code>.</p>

<p>1. Add the necessary dependencies to <code>build.gradle</code>:</p>

<pre class="prettyprint">dependencies {
    // Your other dependencies
    // ...

    compile 'org.flywaydb:flyway-core:{{ site.flywayVersion }}'
    compile 'org.sqldroid:sqldroid:1.0.3'
}</pre>

    <p>2. Make sure that your migrations are included as assets (notice that assets have to be declared in the project itself and not in a dependency. But you can use reference e.g. <code>'../lib/src/main/resources'</code> to use the resources of a lib project)</p>

<pre class="prettyprint">android {
    // SDK, config, buildTypes, etc
    // ...

    sourceSets {
        // Place your db/migration folder here
        main { assets.srcDirs = ['src/main/assets'] }
    }

    // ...
}</pre>

<p>3. Include the setup in your main activity onCreate or application onCreate:</p>

<pre class="prettyprint">import org.flywaydb.core.Flyway;
import org.flywaydb.core.api.android.ContextHolder;
import org.sqldroid.DroidDataSource;

...

DroidDataSource dataSource = new DroidDataSource(getPackageName(), "...");
ContextHolder.setContext(this);
Flyway flyway = new Flyway();
flyway.setDataSource(dataSource);
flyway.migrate();</pre>

<h2 id="spring">Spring Configuration</h2>

<p>As an alternative to the programmatic configuration, here is how you can configure and start Flyway in a typical
    Spring application: </p>
<pre class="prettyprint">&lt;bean id=&quot;flyway&quot; class=&quot;org.flywaydb.core.Flyway&quot; init-method=&quot;migrate&quot;&gt;
    &lt;property name=&quot;dataSource&quot; ref=&quot;...&quot;/&gt;
    ...
&lt;/bean&gt;

&lt;!-- The rest of the application (incl. Hibernate) --&gt;
&lt;!-- Must be run after Flyway to ensure the database is compatible with the code --&gt;
&lt;bean id=&quot;sessionFactory&quot; class=&quot;...&quot; depends-on=&quot;flyway&quot;&gt;
    ...
&lt;/bean&gt;</pre>

<p class="next-steps">
    <a class="btn btn-primary" href="/documentation/api/hooks">API: Hooks <i class="fa fa-arrow-right"></i></a>
</p>