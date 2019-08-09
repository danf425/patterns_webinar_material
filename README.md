Simple idea: Highlight policyfiles and end on the path toward more modern patterns (effortless). Instead of telling the audience why something is better and why we are opinonated about x,y, and z. Actually go through the pain in real-time.  
  
- Start with basic knife, pre-berkshelf (Notes: I hope no-one is doing this anymore, but it’s good to go over why we start making upgrades to our processes. Also don’t spend more than 3 minutes on this)   
- Fix knife problems with berkshelf (dependency solving and having kitchen run local tests to enable TDD)… Add some extra cookbooks w/ attributes and start making the job difficult for Berks.  
- Maybe talk about role cookbooks, but even if someone is using role cookbooks, they are still relying on berks for the deps-solv.  
- Introduce policyfiles to handle more elaborate run-lists, attributes, and dep-solver on build rather than run time.  
	- I’ll probably run all tests locally, but once a proper policy lock file is generated, I want to run it through a proper pipeline. Therefore, guaranteeing the exact same thing that happens in local can happen in prod. (Immutable artifact)  
  
- Finish highlighting the potential of effortless where:  
	- the chef server can be let go, and boot strapping becomes a thing of the past. (Streamlining the process so that a single pipeline can be used for all changes)  
	- Contract between infra -vs- apps are obvious  
	- etc.  

  
  
# Different Patterns

Objective: get yourself a hardened Centos OS (Maybe do other stuff)

### 1_pureknife: 
 - Approach:: Do everything manual. download stuff from supermarket because theres no dependency solving  
 - Still need this to converge... never used kitchen without Berkshelf...  

By default hardening will fail because os-hardening can't be found.
0. kitchen converge (this will fail because it has dependencies)
1. "Install" `os-hardening` from the supermarket:  
     - Go to cookbooks directory: `cd ..`  
     -`knife supermarket download os-hardening -o .`  
     -`tar xvzf os-hardening.tar.gz`
     - Then you would have to do a `knife cookbook upload` and upload it to your server. But at the point you are not even TDDing (This will not run with kitchen so let's bypass this)



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
  
  - Created with Chef workstation 0.7.4  
  - Highlight difference in structure:   
      - No more roles and environments  
      - We now have a policyfiles directory  
  - I've created a new .kitchen.yml file at the root of the repo   
      - location of .kitchen.yml: `3_policyfiles/.kitchen.yml`   
      - Added path within yml: `policyfile: policyfiles/base.rb`  
  - I've create a new policyfile under policyfiles/base.rb
      - 1 change: added path to hardening cookbook


PolicyFiles Instructions:  
- Add attributes:   
```
# Override attributes           
default['hardening'] = { }
```