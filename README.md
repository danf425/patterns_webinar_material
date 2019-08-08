# Different Patterns

Objective: get yourself a hardened Centos OS



### 1_pureknife: 
 - Approach:: Do everything manual. download stuff from supermarket because theres no dependency solving  
 - Still need this to converge... never used kitchen without Berkshelf...  

 ### 2_berks:
  - Approach:: Add the Berksfile and everything now works.  
  - This is setup for now., but need to make it break to introduct polictyfiles  
```
Contents:
- 2 recipes and 1 auditd.conf file needed within the remediation.
- Berksfile is added 
- Dependency is input within metadata.rb
```



### 3_policyfiles:
  - Approach: Fix the above
  - ** Still need to get this to converge with the initial setup.