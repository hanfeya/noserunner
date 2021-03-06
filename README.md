noserunner 0.0.2
==========

runner based on python nose testing framework



### Dependency
    sudo pip install nose
    
### Help
    $ cd noserunner
    $ python runtests.py -h
  
### Command-line
    usage:
	python runtests.py [-h|--help] [--cycle CYCLE] [--reportserver] [,[argv]]


    Process the paramters of runtests
    optional arguments:
	    -h, --help            Show this help message and exit

	    --cycle CYCLE         Set the number(int) of cycle. Execute test with a specified number of cycle. Default is 1
	    
	    --plan PLAN           Set the absolute path or relative path of test plan file. If not provide this option. The "plan" file in current directory will be used as default

	    --duration DURATION   The minumum test duration before ending the test.
					          Here format must follow next format: xxDxxHxxMxxS.
					          e.g. --duration=2D09H30M12S, which means 2 days, 09 hours, 30 minutes and 12 seconds

	    --reportserver        Enable the report server feature. Default is disable
	    
        --server-config       Specify the path of server configuration file.
                              If not provide this option. The "server.config" file in current directory will be used as default
                              
        --device-config       Specify the path of device configuration file.
                              If not provide this option. The "device.config" file in current directory will be used as default
                              
	    --verbosity           Default is 2. set the level(1~5) of verbosity to get the help string of every test and the result
	    
	    argv                  Additional arguments accepted by nose
    e.g:
        python runtests.py --cycle 10                             #run test with 10 cycles
        python runtests.py --duration 2d                          #run test with 2 days      
        python runtests.py --cycle 2 --duration 4h                #run test with 10 cycles and expect to finish within 4 hours
        python runtests.py --cycle 10 --plan path_of_my_plan_file #specify the location of test plan file
        python runtests.py --cycle 10 --reportserver              #enable to upload result to report server
  
### TestCaseContext instance provided by nose plugin

    test case extends from unittest.TestCase is able to get TestCaseContext obj during nose run time.
     
    """
    def testMethod(self):
        ctx = self.contexts 
        user_log_dir_path = ctx.user_log_dir
        device_id = ctx.device_config['deviceid']
        
    """
    function test case is able to get TestCaseContext obj during nose run time.
     
    """
    def testMethod():
        ctx = contexts 
        user_log_dir_path = ctx.user_log_dir
        device_id = ctx.device_config['deviceid']
        
    """

### Make entire logcat log
    how to:
        python makelog.py --help
        
    e.g:
        python makelog.py -d path_of_report/2014-04-02_23:38:32 -f entire.log

### Demo

    ├── client.py                                       #nose plugin module
    ├── planloader.py                                   #nose plugin module
    ├── reporter.py                                     #nose plugin module
    ├── makelog.py                                      #make an entire log file based on report folder
    ├── runtests.py                                     #launch script
    ├── scripts                                         #test case package
    │   ├── __init__.py
    │   ├── pics                                        #test case related sources
    │   │   ├── browser.BrowserTest.testOpenBrowser
    │   │   │   ├── baidu_logo.png
    │   │   │   └── baidu_logo.(x267y267w554h206).png
    │   │   └── phone.PhoneTest.testCall
    │   └── testcases                                   #unittest test case package
    │       ├── __init__.py 
    │       ├── browser.py                              #test case for browser
    │       ├── phone.py                                #test case for phone
    └── server.config                                   #config file (server, account, device...)
    ├── plan                                            #test case plan

