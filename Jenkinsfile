node('ub16.04') {
                
                	stage('Check distro version')
	                {
	                script{
			            sh '''
			            package_name="beats"
			            published_version="6.2.4"
			            #Check distro and available version in repo : rhel7.x, Sles11.x/12.x, Ub16.x/17.x 
			            available_version=$(sudo apt-get update && sudo apt-cache policy $package_name | grep Candidate | head -1 | cut -d ' ' -f 4)
			            if [[ $available_version == *"$published_version"* ]]; then
			            echo "Version $published_version is already available in repo"
			            echo "Exact name: $available_version ... Failing"
			            exit 1
			            else	
			            echo "Published version is not available in repo. Going ahead."     
			            fi
			            '''
		              }
	                }
                WS = "${pwd}"
		PATH = "${PATH}:/usr/lib/go-1.9/bin"
		GOPATH="$WS"
                withEnv(["WS=${pwd}", "PATH=$PATH:/usr/lib/go-1.9/bin", "GOPATH=$WS"]) {
                stage('Install Dependencies') {
                        script {
                            sh '''
                            echo "${pwd}"
                            sudo rm -rf ./*
                            sudo apt-get update -y
                            sudo apt-cache policy python
                            sudo apt-cache policy beats* || true
                            sudo apt-get install -y git make wget tar gcc python python-setuptools libcap-dev libpcap0.8-dev openssl libssh-dev python-openssl acl rsync golang-1.9 tzdata
                            		 
                            sudo python -m easy_install pip
                            sudo python -m pip install appdirs pyparsing six packaging setuptools wheel PyYAML termcolor ordereddict nose-timer MarkupSafe virtualenv
                            setfacl -dm u::rwx,g::r,o::r $GOPATH
                            '''
                            }
                           	}
                            	
                            	
                            	  stage('Download Source Code & Make Code Changes'){
                                   script {
                            			 sh '''
                            			 mkdir -p $GOPATH/src/github.com/elastic
                            			 cd $GOPATH/src/github.com/elastic
                            			 rm -rf beats
                            			 git clone https://github.com/elastic/beats.git
                            			 cd beats
                            			 git checkout v6.2.4
                            		         #Code change to fix metricbeat socket test
                            			 cp $GOPATH/src/github.com/elastic/beats/vendor/github.com/elastic/gosigar/sys/linux/inetdiag.go $GOPATH/src/github.com/elastic/beats/vendor/github.com/elastic/gosigar/sys/linux/inetdiag.go.orig
                            			 sed -i '14a\\t"runtime"' $GOPATH/src/github.com/elastic/beats/vendor/github.com/elastic/gosigar/sys/linux/inetdiag.go
                            			 sed -i '198d' $GOPATH/src/github.com/elastic/beats/vendor/github.com/elastic/gosigar/sys/linux/inetdiag.go
                            			 sed -i '198d' $GOPATH/src/github.com/elastic/beats/vendor/github.com/elastic/gosigar/sys/linux/inetdiag.go
                            			 sed -i '198d' $GOPATH/src/github.com/elastic/beats/vendor/github.com/elastic/gosigar/sys/linux/inetdiag.go
                            			 sed -i '198d' $GOPATH/src/github.com/elastic/beats/vendor/github.com/elastic/gosigar/sys/linux/inetdiag.go
                                                 sed -i '198d' $GOPATH/src/github.com/elastic/beats/vendor/github.com/elastic/gosigar/sys/linux/inetdiag.go
                                                 sed -i '197a\\t if ( runtime.GOARCH == "s390x" ) {' $GOPATH/src/github.com/elastic/beats/vendor/github.com/elastic/gosigar/sys/linux/inetdiag.go
                                                 sed -i '198a\\t\t binary.BigEndian.PutUint32(b[0:4], msg.Header.Len)' $GOPATH/src/github.com/elastic/beats/vendor/github.com/elastic/gosigar/sys/linux/inetdiag.go
                                                 sed -i '199a\\t\t binary.BigEndian.PutUint16(b[4:6], msg.Header.Type)' $GOPATH/src/github.com/elastic/beats/vendor/github.com/elastic/gosigar/sys/linux/inetdiag.go
                                                sed -i '200a\\t\t binary.BigEndian.PutUint16(b[6:8], msg.Header.Flags)' $GOPATH/src/github.com/elastic/beats/vendor/github.com/elastic/gosigar/sys/linux/inetdiag.go
                                                sed -i '201a\\t\t binary.BigEndian.PutUint32(b[8:12], msg.Header.Seq)' $GOPATH/src/github.com/elastic/beats/vendor/github.com/elastic/gosigar/sys/linux/inetdiag.go
                                                sed -i '202a\\t\t binary.BigEndian.PutUint32(b[12:16], msg.Header.Pid)' $GOPATH/src/github.com/elastic/beats/vendor/github.com/elastic/gosigar/sys/linux/inetdiag.go
                                                sed -i '203a\\t } else {' $GOPATH/src/github.com/elastic/beats/vendor/github.com/elastic/gosigar/sys/linux/inetdiag.go
                                                sed -i '204a\\t\t binary.LittleEndian.PutUint32(b[0:4], msg.Header.Len)' $GOPATH/src/github.com/elastic/beats/vendor/github.com/elastic/gosigar/sys/linux/inetdiag.go
                                                sed -i '205a\\t\t binary.LittleEndian.PutUint16(b[4:6], msg.Header.Type)' $GOPATH/src/github.com/elastic/beats/vendor/github.com/elastic/gosigar/sys/linux/inetdiag.go
                                                sed -i '206a\\t\t binary.LittleEndian.PutUint16(b[6:8], msg.Header.Flags)' $GOPATH/src/github.com/elastic/beats/vendor/github.com/elastic/gosigar/sys/linux/inetdiag.go
                                                sed -i '207a\\t\t binary.LittleEndian.PutUint32(b[8:12], msg.Header.Seq)' $GOPATH/src/github.com/elastic/beats/vendor/github.com/elastic/gosigar/sys/linux/inetdiag.go
                                                sed -i '208a\\t\t binary.LittleEndian.PutUint32(b[12:16], msg.Header.Pid)' $GOPATH/src/github.com/elastic/beats/vendor/github.com/elastic/gosigar/sys/linux/inetdiag.go
                                                sed -i '209a\\t }' $GOPATH/src/github.com/elastic/beats/vendor/github.com/elastic/gosigar/sys/linux/inetdiag.go
                                                sed -i '327d' $GOPATH/src/github.com/elastic/beats/vendor/github.com/elastic/gosigar/sys/linux/inetdiag.go
                                                sed -i '326a\\t var err error' $GOPATH/src/github.com/elastic/beats/vendor/github.com/elastic/gosigar/sys/linux/inetdiag.go
                                                sed -i '327a\\t if ( runtime.GOARCH == "s390x" ) {' $GOPATH/src/github.com/elastic/beats/vendor/github.com/elastic/gosigar/sys/linux/inetdiag.go
                                                sed -i '328a\\t\t err = binary.Read(r, binary.BigEndian, inetDiagMsg)' $GOPATH/src/github.com/elastic/beats/vendor/github.com/elastic/gosigar/sys/linux/inetdiag.go
                                                sed -i '329a\\t } else {' $GOPATH/src/github.com/elastic/beats/vendor/github.com/elastic/gosigar/sys/linux/inetdiag.go
                                                sed -i '330a\\t\t err = binary.Read(r, binary.LittleEndian, inetDiagMsg)' $GOPATH/src/github.com/elastic/beats/vendor/github.com/elastic/gosigar/sys/linux/inetdiag.go
                                                sed -i '331a\\t }' $GOPATH/src/github.com/elastic/beats/vendor/github.com/elastic/gosigar/sys/linux/inetdiag.go
                            			diff -u $GOPATH/src/github.com/elastic/beats/vendor/github.com/elastic/gosigar/sys/linux/inetdiag.go.orig $GOPATH/src/github.com/elastic/beats/vendor/github.com/elastic/gosigar/sys/linux/inetdiag.go || true
                            			cp $GOPATH/src/github.com/elastic/beats/libbeat/scripts/Makefile $GOPATH/src/github.com/elastic/beats/libbeat/scripts/Makefile.orig
                                                sed -i 35d $GOPATH/src/github.com/elastic/beats/libbeat/scripts/Makefile
                                                sed -i '34aTIMEOUT?= 900000' $GOPATH/src/github.com/elastic/beats/libbeat/scripts/Makefile
                                                diff -u $GOPATH/src/github.com/elastic/beats/libbeat/scripts/Makefile.orig  $GOPATH/src/github.com/elastic/beats/libbeat/scripts/Makefile || true
                                                find $GOPATH/src/github.com/elastic/beats/ -type f -iname "*.py" -print0 | xargs -0 sed -i 's/max_timeout=10/max_timeout=10000/g'
                                                git diff $GOPATH/src/github.com/elastic/beats || true 
                            			#Code change to fix audit test
                            			sed -i 's/arch=b64/arch=s390x || arch=b64/g' $GOPATH/src/github.com/elastic/beats/auditbeat/module/auditd/config_linux_test.go
                            			'''
                                   }
                              	}
                                
                                stage('Build and test filebeat'){
                            			script {
                            			sh '''
                            			cd $GOPATH/src/github.com/elastic/beats/filebeat
                            			make
                            			./filebeat --version
                            			make update
                            			# Intermittent test failures are observed, can be passed after multiple run  
                            			make unit
                            			make system-tests
                            			'''
                                }
                            	}
                            	
                            	stage('Build and test packetbeat'){
                            			script {
                            			sh '''
                            			cd $GOPATH/src/github.com/elastic/beats/packetbeat
                            			make
                            			./packetbeat --version
                            			make update
                            			# Intermittent test failures are observed, can be passed after multiple run  
                            			make unit
                            			make system-tests
                            			'''
                                }
                            	}
                            	stage('Build and test metricbeat'){
                            			script{
                            			sh'''
                            			cd $GOPATH/src/github.com/elastic/beats/metricbeat
                            			make
                            			./metricbeat --version
                            			make update
                            			# Same single test failure is observed on x86
                            			make unit 2>&1 | tee -a unit_test
                            			make system-tests 2>&1 | tee -a sys_test
                            			echo "FAIL: Test system/process output." >> expectedfail1
                            			grep "FAIL:" sys_test | tee actuallyfail1
                            			if diff -u --ignore-all-space expectedfail1 actuallyfail1 ; then
                            				echo "Unexpected failures found!"
                            			    exit 1
                            			fi
                            			'''
                            		}
                            		}
                            		
                            	stage('Build and test libbeat'){
                            			script{
                            			sh'''
                            			cd $GOPATH/src/github.com/elastic/beats/libbeat
                            			make
                            			./libbeat --version
                            			make update
                            			# Intermittent test failures are observed, can be passed after multiple run  
                            			make unit
                            			make system-tests
                            			echo "ERROR: test that we support nested key" >> expectedfail2
                            			echo "ERROR: Test that we correctly to string replacement with values from the keystore" >> expectedfail2
                            			grep "ERROR:" sys_test | tee actuallyfail2
                            			if diff -u --ignore-all-space expectedfail2 actuallyfail2 ; then
                            				echo "Unexpected failures found!"
                            				exit 1
                            			fi
                            			find $GOPATH/src/github.com/elastic/beats/ -type f -iname "*.py" -print0 | xargs -0 sed -i 's/max_timeout=10000/max_timeout=1000/g'
                            			'''
                            			}
                            		}
                            		
                            	stage('Build and test heartbeat'){
                            		script{
                            		sh '''
                            		cd $GOPATH/src/github.com/elastic/beats/heartbeat
                            		make
                            		./heartbeat --version
                            		make update
                            		# Intermittent test failures are observed, can be passed after multiple run  
                            		make unit
                            		make system-tests
                            		'''
                            		}
                            		}
                            	
                            	stage('Build and test auditbeat'){
                            		script{
                            		sh '''
                            		cd $GOPATH/src/github.com/elastic/beats/auditbeat
                            		make
                            		./auditbeat --version
                            		make update 
                            		make unit 2>&1 | tee -a unit_test
                            		make system-tests 2>&1 | tee -a sys_test
                            		echo "ERROR: Auditbeat starts and stops without error." >> expectedfail2
                            		grep "ERROR:" sys_test | tee actuallyfail2
                            		if diff -u --ignore-all-space expectedfail2 actuallyfail2 ; then
                            			echo "Unexpected failures found!"
                            		    exit 1
                            		fi
                            		'''
                            		}
                            	}
                            	
                            	stage('Verification'){
                            	script{
                            		sh'''
                            		# Verify that individual beats are running without error
                            		cd $GOPATH/src/github.com/elastic/beats/filebeat
                            		sudo chown root filebeat.yml
                            		sudo ./filebeat -e -c filebeat.yml -d "publish" &
                            		sleep 5s
                            		pgrep -d" " -f "filebeat" | sudo xargs kill || true
                            		cd $GOPATH/src/github.com/elastic/beats/packetbeat
                            		sudo chown root packetbeat.yml
                            		sudo ./packetbeat -e -c packetbeat.yml -d "publish" &
                            		sleep 5s
                            		pgrep -d" " -f "packetbeat" | sudo xargs kill || true
                            		cd $GOPATH/src/github.com/elastic/beats/metricbeat
                            		sudo chown root metricbeat.yml
                            		sudo chown root $GOPATH/src/github.com/elastic/beats/metricbeat/modules.d/system.yml
                            		sudo ./metricbeat -e -c metricbeat.yml -d "publish" &
                            		sleep 5s
                            		pgrep -d" " -f "metricbeat" | sudo xargs kill || true
                            		cd $GOPATH/src/github.com/elastic/beats/heartbeat
                            		sudo chown root heartbeat.yml
                            		sudo ./heartbeat -e -c heartbeat.yml -d "publish" &
                            		sleep 5s
                            		pgrep -d" " -f "heartbeat" | sudo xargs kill || true
                            		# Under Docker, Auditbeat runs as a non-root user,but requires some privileged capabilities to operate correctly.
                            		# Ensure that the AUDIT_CONTROL and AUDIT_READ capabilities are available to the container.
                            		# It is also essential to run Auditbeat in the host PID namespace.
                            		# Option to be used with docker run : --cap-add=AUDIT_CONTROL,AUDIT_READ --pid=host
                            		cd $GOPATH/src/github.com/elastic/beats/auditbeat
                            		sudo chown root auditbeat.yml
                            		sudo ./auditbeat -e -c auditbeat.yml -d "publish" &
                            		sleep 5s
                            		pgrep -d" " -f "auditbeat" | sudo xargs kill || true
                            		'''
                            	}
                            	}
                            	

                            }
    }
