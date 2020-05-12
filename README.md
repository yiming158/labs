
import os,sys,threading,requests,time
from queue import Queue




print("current PID: ",os.getpid())
print("the OS is: ",sys.platform)

if(sys.platform)=="linux":
    print("loadavg: ",os.getloadavg())
    

min_1, min_5, min_15 = os.getloadavg()
print("5 min loadavg: ",min_5)
print("CPU count: ",os.cpu_count())
if((os.cpu_count()-min_5)<1):
    sys.exit()
print("**************************************************************")
  
def make_request(url):
    
    resp = requests.get(url)
    with print_lock:
        print(format(threading.current_thread().name))
        print(format(resp.status_code))

def m_queue():
    while True:

         
        current_url = url_queue.get()

    
        make_request(current_url)

        
        url_queue.task_done()

if __name__ == '__main__':

    
    number_of_threads = 3
    
    print_lock = threading.Lock()
    
    
    url_queue = Queue()

    
    urls = [
    'https://api.github.com​', 'http://bilgisayar.mu.edu.tr/​',
'https://www.python.org/​', 'http://akrepnalan.com/ceng2034​',
'https://github.com/caesarsalad/wow​'] 

   
    for i in range(number_of_threads):

        
        t = threading.Thread(target=m_queue)

        
        t.daemon = True
        t.start()
    
    start = time.time()

    
    for current_url in urls:
        url_queue.put(current_url)

    
    url_queue.join()

    print(format(time.time() - start))


    


     
