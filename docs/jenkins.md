# Jenkins

## List Credentilas

### List credentails of jenkins from global

Script to include SSH credentials contained within folders.

!!! note "Run in script console"

``` sh
import com.cloudbees.plugins.credentials.Credentials
Set<Credentials> allCredentials = new HashSet<Credentials>();

def creds = com.cloudbees.plugins.credentials.CredentialsProvider.lookupCredentials(
      com.cloudbees.jenkins.plugins.sshcredentials.impl.BasicSSHUserPrivateKey
);

for (c in creds) {
      println(c.id + ": \n passphrase: " + c.getPassphrase() + "\n" + c.getPrivateKey())
}
```

!!! tip "List all credentails of all folder"

    ``` sh
    import com.cloudbees.plugins.credentials.Credentials

    Set<Credentials> allCredentials = new HashSet<Credentials>();

    def creds = com.cloudbees.plugins.credentials.CredentialsProvider.lookupCredentials(
        com.cloudbees.jenkins.plugins.sshcredentials.impl.BasicSSHUserPrivateKey
    );

    allCredentials.addAll(creds)

    Jenkins.instance.getAllItems(com.cloudbees.hudson.plugins.folder.Folder.class).each{ f ->
    creds = com.cloudbees.plugins.credentials.CredentialsProvider.lookupCredentials(
        com.cloudbees.jenkins.plugins.sshcredentials.impl.BasicSSHUserPrivateKey, f)
    allCredentials.addAll(creds)
    }

    for (c in allCredentials) {
        println(c.id + ": \n passphrase: " + c.getPassphrase() + "\n" + c.getPrivateKey())
    }
    ```

* Here are some [Video Tutorials and additional learning materials](https://www.jenkins.io/doc/book/managing/script-console/#video-tutorials-and-additional-learning-materials).

* There are great resources of groovy scripts that you can review and use for inspiration at [Example Groovy scripts](https://www.jenkins.io/doc/book/managing/script-console/#example-groovy-scripts).

* The Javadocs for the APIs that you can call in a groovy script can be found at:
    * https://javadoc.jenkins.io/
    * https://javadoc.jenkins.io/plugin/
    * [Custom Plugins: APIs and Javadocs of CloudBees Jenkins Enterprise plugins](https://support.cloudbees.com/hc/en-us/articles/228175367)
