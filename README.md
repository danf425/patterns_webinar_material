# Different Patterns

Objective: get yourself a hardened Centos OS



### 1_pureknife: 
 - Approach:: Do everything manual. download stuff from supermarket because theres no dependency solving  
 - Still need this to converge... never used kitchen without Berkshelf...  


 ### 2_berks:
  - Approach:: Add the Berksfile and everything now works.  
  Status: Currently converges the hardening cookbook
  To Do: Add something that breaks berks, but works on policyfiles
```
Contents:
- 2 recipes and 1 auditd.conf file needed within the remediation.
- Berksfile is added 
- Dependency is input within metadata.rb
- RunList has to be specified in kitchen.yml (Much how this would be attached to a role)
```


### 3_policyfiles:
  - Approach: Fix the above
  Status: Converges the same as berks. (Hardening cookbook)