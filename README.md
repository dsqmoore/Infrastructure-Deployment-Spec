Description
===========
This project aims to define a tool- and cloud-independent specification to automate infrastructure provisioning, which, together with a Configuration Managment System like [Chef](http://wiki.opscode.com/display/chef/Home) or [Puppet](http://projects.puppetlabs.com/projects/puppet/wiki) should for the first time fully deliver on the promise of "Infrastructure as code".

Amazon's Web Services [recent outage](http://agilesysadmin.net/ec2-outage-lessons) has paradoxically highlighted the need for a tool like [AWS CouldFormation](http://aws.amazon.com/documentation/cloudformation/) that is vendor independent.

There are already Open Source cloud-agnostic libraries for cloud APIs ([Fog](https://github.com/geemus/fog), [libcloud](http://incubator.apache.org/libcloud/)...), and several tools that make use of it (Chef's knife, [Spiceweasel](https://github.com/mattray/spiceweasel)) but a tool-independent infrastructure specification is still missing.

An example of how the specification could look like (from example.json):

```javascript
{
    "speficication_version": "0.1",
    "deployment_version": "1.0",
    "name": "Web App",
    "description": "A full Web application, master DB and master slave deployment",
    "nodes": [
        {
            "name": "Master DB",
            "description": "This node will host the Master DB",
            "provider": "Rackspace",
            "image": "49",
            "machine": "2",
            "zone": "1",
            "roles": [
                "role[master_db]"
            ],
            "step": 1
        },
        {
            "name": "Slave DB",
            "description": "This node will host the Slave DB",
            "provider": "Rackspace",
            "image": "49",
            "machine": "2",
            "zone": "1",
            "roles": [
                "role[slave_db]"
            ],
            "step": 2
        },
        {
            "name": "WebApp",
            "description": "The Apache web server and our App",
            "provider": "EC2",
            "image": "ami-014da868",
            "machine": "c1.xlarge",
            "zone": "us-east-1",
            "roles": [
                "role[frontend]"
            ],
            "step": 2
        }
    ]
}
```

Go to the [Wiki](https://github.com/tobami/Infrastructure-Deployment-Spec/wiki) and help in defining this specification!

This work is licensed under the [Creative Commons Attribution-ShareAlike 3.0 Unported License](http://creativecommons.org/licenses/by-sa/3.0/)
