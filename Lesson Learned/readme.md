
## 1. The Power of `file://`

One of the most useful AWS CLI features I learned during this project was the ability to reference local files using the `file://` prefix.

This was especially valuable when working with:

* IAM Trust Policies
* Launch Template JSON files
* User Data scripts
* Configuration files

Using `file://` allowed complex configurations to be stored in reusable files rather than typing long JSON strings directly into the terminal.

This improved:

* Readability
* Reusability
* Troubleshooting
* Configuration management

---

## 2. Launch Template Revisions Matter

I learned that Launch Templates are versioned resources.

Updating a Launch Template does not automatically update existing EC2 instances or Auto Scaling Groups. New versions must be created and the Auto Scaling Group must be configured to use the desired version.

This became important when modifying:

* User Data scripts
* IAM Instance Profiles
* Security Groups
* AMI selections

Understanding Launch Template versioning helped prevent confusion when troubleshooting deployment issues.

---

## 3. Auto Scaling Is Not Instant

One lesson learned during validation was that Auto Scaling replacement takes time.

When an EC2 instance is terminated, the Auto Scaling Group does not immediately provide a fully operational replacement instance.

The replacement process includes:

1. Launching a new EC2 instance
2. Running User Data scripts
3. Installing required software
4. Starting services
5. Passing Load Balancer health checks
6. Registering as a healthy target

This delay can impact application availability if not properly planned for.

The experience highlighted the importance of:

* Desired Capacity settings
* Health Checks
* Warm-up periods
* Redundancy across multiple Availability Zones

A replacement instance may launch quickly, but becoming fully operational takes additional time.
