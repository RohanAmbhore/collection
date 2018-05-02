<a href="https://dev.mysql.com/doc/refman/8.0/en/password-management.html">https://dev.mysql.com/doc/refman/8.0/en/password-management.html</a><div id="articleHeader"><h1>6.3.8 Password Management</h1></div>
<p>
      MySQL supports these password-management capabilities:
</p>
<div>
<ul><li><p>
          Password expiration, to require passwords to be changed
          periodically
        </p></li><li><p>
          Password reuse restrictions, to prevent old passwords from
          being chosen again
        </p></li><li><p>
          Password strength assessment, to require strong passwords
</p></li></ul>
</div>
<p>
      The following sections describe password expiration and
      reuse-restriction capabilities. Password strength assessment is
      implemented using the <code>validate_password</code> plugin;
      see <a href="validate-password.html" title="6.5.3 The Password Validation Component" target="_blank">Section 6.5.3, “The Password Validation Component”</a>.
</p>


<div>

<div>
Important
</div>
<p>
        MySQL implements password-reuse restrictions by means of columns
        in the <code>mysql.user</code> system table and a
        <code>mysql.password_history</code> system table that are
        new in MySQL 8.0.3. If you upgrade to 8.0.3 or higher release
        from an earlier version, you must incorporate these system
        database changes. Otherwise, the server writes these messages to
        the error log during the startup process:
      </p><div><pre><code>[ERROR] Column count of mysql.user is wrong. Expected
49, found 47. The table is probably corrupted
[Warning] ACL table mysql.password_history missing.
Some operations may fail.</code></pre></div><p>
        To correct the issue, run <a href="mysql-upgrade.html" title="4.4.5 mysql_upgrade — Check and Upgrade MySQL Tables" target="_blank"><strong>mysql_upgrade</strong></a> and
        restart the server. Until this is done, <em>password
        changes are not possible.</em>
</p>

<div>
<div>
<div>
<div>
<h4>Password Expiration Policy</h4>

</div>




<p>
        MySQL enables database administrators to expire account
        passwords manually, and to establish a policy for automatic
        password expiration. It is possible to establish expiration
        policy globally, as well as on a per-account basis. These
        capabilities apply to accounts that use a MySQL built-in
        authentication plugin (<code>mysql_native_password</code>,
        <code>sha256_password</code>, or
        <code>caching_sha2_password</code>). For accounts that use
        plugins that perform authentication against an external
        credential system, password expiration must be handled
        externally as well.
      </p><p>
        To expire an account password manually, use the
        <a href="alter-user.html" title="13.7.1.1 ALTER USER Syntax" target="_blank"><code>ALTER USER</code></a> statement:
      </p><div><pre><code>ALTER USER 'jeffrey'@'localhost' PASSWORD EXPIRE;</code></pre></div><p>
        This operation marks the password expired in the corresponding
        <code>mysql.user</code> table row.
      </p><p>
        Password expiration according to policy is automatic and is
        based on password age, which for a given account is assessed
        from the date and time of its most recent password change. The
        <code>mysql.user</code> table indicates for each account
        when its password was last changed, and the server automatically
        treats the password as expired at client connection time if its
        age is greater than its permitted lifetime. This works with no
        explicit manual password expiration.
      </p><p>
        To establish automatic password-expiration policy globally, use
        the <a href="server-system-variables.html#sysvar_default_password_lifetime" target="_blank"><code>default_password_lifetime</code></a>
        system variable. Its default value is 0, which disables
        automatic password expiration. If the value of
        <a href="server-system-variables.html#sysvar_default_password_lifetime" target="_blank"><code>default_password_lifetime</code></a> is a
        positive integer <em><code>N</code></em>, it indicates the
        permitted password lifetime, such that passwords must be changed
        every <em><code>N</code></em> days.
      </p><p>
        Examples:
</p>
<div>
<ul><li><p>
            To establish a global policy that passwords have a lifetime
            of approximately six months, start the server with these
            lines in a server <code>my.cnf</code> file:
          </p><div><pre><code>[mysqld]
default_password_lifetime=180</code></pre></div></li><li><p>
            To establish a global policy such that passwords never
            expire, set
            <a href="server-system-variables.html#sysvar_default_password_lifetime" target="_blank"><code>default_password_lifetime</code></a>
            to 0:
          </p><div><pre><code>[mysqld]
default_password_lifetime=0</code></pre></div></li><li><p>
            <a href="server-system-variables.html#sysvar_default_password_lifetime" target="_blank"><code>default_password_lifetime</code></a>
            can also be set and persisted at runtime:
          </p><div><pre><code>SET PERSIST default_password_lifetime = 180;
SET PERSIST default_password_lifetime = 0;</code></pre></div><p>
            <a href="set-variable.html" title="13.7.5.1 SET Syntax for Variable Assignment" target="_blank"><code>SET
            PERSIST</code></a> sets the value for the running MySQL
            instance. It also saves the value to be used for subsequent
            server restarts; see <a href="set-variable.html" title="13.7.5.1 SET Syntax for Variable Assignment" target="_blank">Section 13.7.5.1, “SET Syntax for Variable Assignment”</a>. To
            change a value only for the running MySQL instance without
            saving it for subsequent restarts, use the
            <code>GLOBAL</code> keyword rather than
            <code>PERSIST</code>.
</p></li></ul>

<p>
        To establish password-expiration policy for individual accounts,
        use the <code>PASSWORD EXPIRE</code> options of the
        <a href="create-user.html" title="13.7.1.3 CREATE USER Syntax" target="_blank"><code>CREATE USER</code></a> and
        <a href="alter-user.html" title="13.7.1.1 ALTER USER Syntax" target="_blank"><code>ALTER USER</code></a> statements. See
        <a href="create-user.html" title="13.7.1.3 CREATE USER Syntax" target="_blank">Section 13.7.1.3, “CREATE USER Syntax”</a>, and <a href="alter-user.html" title="13.7.1.1 ALTER USER Syntax" target="_blank">Section 13.7.1.1, “ALTER USER Syntax”</a>.
      </p><p>
        Example account-specific expiration statements:
</p>
<div>
<ul><li><p>
            Require the password to be changed every 90 days:
          </p><div><pre><code>CREATE USER 'jeffrey'@'localhost' PASSWORD EXPIRE INTERVAL 90 DAY;
ALTER USER 'jeffrey'@'localhost' PASSWORD EXPIRE INTERVAL 90 DAY;</code></pre></div></li><li><p>
            Disable password expiration:
          </p><div><pre><code>CREATE USER 'jeffrey'@'localhost' PASSWORD EXPIRE NEVER;
ALTER USER 'jeffrey'@'localhost' PASSWORD EXPIRE NEVER;</code></pre></div></li><li><p>
            Defer to the global expiration policy:
          </p><div><pre><code>CREATE USER 'jeffrey'@'localhost' PASSWORD EXPIRE DEFAULT;
ALTER USER 'jeffrey'@'localhost' PASSWORD EXPIRE DEFAULT;</code></pre></div></li></ul>

<p>
        When a client successfully connects, the server determines
        whether the account password has expired:
</p>
<div>
<ul><li><p>
            The server checks whether the password has been manually
            expired.
          </p></li><li><p>
            Otherwise, the server checks whether the password age is
            greater than its permitted lifetime according to the
            automatic password expiration policy. If so, the server
            considers the password expired.
</p></li></ul>
</div>
<p>
        If the password is expired (whether manually or automatically),
        the server either disconnects the client or restricts the
        operations permitted to it (see
        <a href="expired-password-handling.html" title="6.3.9 Server Handling of Expired Passwords" target="_blank">Section 6.3.9, “Server Handling of Expired Passwords”</a>). Operations
        performed by a restricted client result in an error until the
        user establishes a new account password:
      </p><div><pre><code>mysql&gt; SELECT 1;
ERROR 1820 (HY000): You must reset your password using ALTER USER
statement before executing this statement.

mysql&gt; ALTER USER USER() IDENTIFIED BY '<em>password</em>';
Query OK, 0 rows affected (0.01 sec)

mysql&gt; SELECT 1;
+---+
| 1 |
+---+
| 1 |
+---+
1 row in set (0.00 sec)</code></pre></div><p>
        After the client resets the password, the server restores normal
        access for the session, as well as for subsequent connections
        that use the account. It is also possible for an administrative
        user to reset the account password, but any existing restricted
        sessions for that account remain restricted. A client using the
        account must disconnect and reconnect before statements can be
        executed successfully.
</p>
<div>


<p>
          It is possible to “reset” a password by setting
          it to its current value. As a matter of good policy, it is
          preferable to choose a different password. DBAs can enforce
          non-reuse by establishing an appropriate password-reuse
          policy. See <a href="password-management.html#password-reuse-policy" title="Password Reuse Policy" target="_blank">Password Reuse Policy</a>.
</p>
</div>


<div>
<div>
<div>
<div>
<h4>Password Reuse Policy</h4>

</div>




<p>
        MySQL enables restrictions to be placed on reuse of previous
        passwords. Reuse restrictions can be established based on number
        of password changes, time elapsed, or both. It is possible to
        establish reuse policy globally, as well as on a per-account
        basis. These capabilities apply to accounts that use a MySQL
        built-in authentication plugin
        (<code>mysql_native_password</code>,
        <code>sha256_password</code>, or
        <code>caching_sha2_password</code>). For accounts that use
        plugins that perform authentication against an external
        credential system, reuse restrictions must be handled externally
        as well.
      </p><p>
        The password history for an account consists of passwords it has
        been assigned in the past. MySQL can restrict new passwords from
        being chosen from this history:
</p>
<div>
<ul><li><p>
            If an account is restricted on the basis of number of
            password changes, a new password cannot be chosen from a
            specified number of the most recent passwords. For example,
            if the minimum number of password changes is set to 3, a new
            password cannot be the same as any of the most recent 3
            passwords.
          </p></li><li><p>
            If an account is restricted based on time elapsed, a new
            password cannot be chosen from passwords in the history that
            are newer than a specified number of days. For example, if
            the password reuse interval is set to 60, a new password
            must not be among those previously chosen within the last 60
            days.
</p></li></ul>
</div>
<div>

<p>
          The empty password does not count in the password history and
          is subject to reuse at any time.
</p>
</div>
<p>
        To establish password-reuse policy globally, use the
        <a href="server-system-variables.html#sysvar_password_history" target="_blank"><code>password_history</code></a> and
        <a href="server-system-variables.html#sysvar_password_reuse_interval" target="_blank"><code>password_reuse_interval</code></a> system
        variables. To specify the variable values at server startup,
        define them in your server <code>my.cnf</code> file.
      </p><p>
        Examples:
</p>
<div>
<ul><li><p>
            To prohibit reusing any of the last 6 passwords or passwords
            newer than 365 days, put these lines in your server
            <code>my.cnf</code> file:
          </p><div><pre><code>[mysqld]
password_history=6
password_reuse_interval=365</code></pre></div></li><li><p>
            To set and persist the variables at runtime, use statements
            like this:
          </p><div><pre><code>SET PERSIST password_history = 6;
SET PERSIST password_reuse_interval = 365;</code></pre></div><p>
            <a href="set-variable.html" title="13.7.5.1 SET Syntax for Variable Assignment" target="_blank"><code>SET
            PERSIST</code></a> sets the value for the running MySQL
            instance. It also saves the value to be used for subsequent
            server restarts; see <a href="set-variable.html" title="13.7.5.1 SET Syntax for Variable Assignment" target="_blank">Section 13.7.5.1, “SET Syntax for Variable Assignment”</a>. To
            change a value only for the running MySQL instance without
            saving it for subsequent restarts, use the
            <code>GLOBAL</code> keyword rather than
            <code>PERSIST</code>.
</p></li></ul>

<p>
        To establish password-reuse policy for individual accounts, use
        the <code>PASSWORD HISTORY</code> and <code>PASSWORD
        REUSE INTERVAL</code> options of the
        <a href="create-user.html" title="13.7.1.3 CREATE USER Syntax" target="_blank"><code>CREATE USER</code></a> and
        <a href="alter-user.html" title="13.7.1.1 ALTER USER Syntax" target="_blank"><code>ALTER USER</code></a> statements. See
        <a href="create-user.html" title="13.7.1.3 CREATE USER Syntax" target="_blank">Section 13.7.1.3, “CREATE USER Syntax”</a>, and <a href="alter-user.html" title="13.7.1.1 ALTER USER Syntax" target="_blank">Section 13.7.1.1, “ALTER USER Syntax”</a>.
      </p><p>
        Examples:
</p>
<div>
<ul><li><p>
            Require a minimum of 5 password changes before permitting
            reuse:
          </p><div><pre><code>CREATE USER 'jeffrey'@'localhost' PASSWORD HISTORY 5;
ALTER USER 'jeffrey'@'localhost' PASSWORD HISTORY 5;</code></pre></div></li><li><p>
            Require a minimum of 365 days elapsed before permitting
            reuse:
          </p></li><li><p>
            To combine both types of reuse restrictions, use both
            <code>PASSWORD HISTORY</code> and <code>PASSWORD
            REUSE INTERVAL</code>:
          </p><div><pre><code>CREATE USER 'jeffrey'@'localhost'
  PASSWORD HISTORY 5
  PASSWORD REUSE INTERVAL 365 DAY;
ALTER USER 'jeffrey'@'localhost'
  PASSWORD HISTORY 5
  PASSWORD REUSE INTERVAL 365 DAY;</code></pre></div></li></ul>




