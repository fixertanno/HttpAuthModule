# Http Auth Module
This is Simple Http Authentication HttpModule for ASP.NET (MVC).
- Basic Authentication
- Digest Authentication 
- Restrict IP Address (ip4 or ip6)
- Basic or Digest Authentication don't tounch HttpContext.Current.User.

# Quick start
Get Nuget package.
https://www.nuget.org/packages/HttpAuthModule/

```
PM> Install-Package HttpAuthModule
``` 

After Getting, configure Web.config file.
It's all you do for using HttpAuthModule.

# Configuration
modify Web.config file.

```XML
<appSettings>
	<!--
      [required] Http Authentication Mode.
      - Basic: Basic authentication
      - Digest: Digest authentication
      - None: No authentication -->
    <add key="HttpAuth" value="Basic"/>
    <!-- [optional] default is "SecureZone" -->
    <add key="HttpAuth.Realm" value=""/>
    <!-- [required if http auth on] user1:pass1;user2:pass2;... -->
    <add key="HttpAuth.Credentials" value="hoge:hogepass;foo:foopass;"/>
    <!-- [optional] Digest Auth Nonce Valid Duration Minutes. default is 120 -->
    <add key="HttpAuth.DigestNonceValidDuration" value="120"/>
    <!-- [required if digest auth on] Digest Auth Nonce Salt -->
    <add key="HttpAuth.DigestNonceSalt" value="uht9987bbbSAX" />
    <!--
      [optional] If set, specified IPs are only allowed: otherwize All IPs are allowed.
      value is joined IP Range Combination as following.
      - 10.23.0.0/24
      - 127.0.0.1 (equals to 127.0.0.1/32)
      - 2001:0db8:bd05:01d2:288a:1fc0:0001:0000/16
      - ::1 (equals to ::1/128)
      
      e.g) 127.0.0.1;182.249.0.0/16;182.248.112.128/26;::1
    -->
    <add key="HttpAuth.RestrictIPAddresses" value="127.0.0.1;::1"/>
    <!-- [optional] If set, specified pattern url request skip http auth and IP Restriction. -->
    <add key="HttpAuth.IgnorePathRegex" value="^/Home/Ignore$|^/Ignore\.aspx$"/>
</appSettings>
<system.webServer>
    <modules>
      <add type="HttpAuthModule.HttpAuthModule" name="HttpAuthModule"/>
    </modules>
  </system.webServer>
```

