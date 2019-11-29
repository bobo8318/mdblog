### 1.watchdog:全平台监测工具

```
import sys
import time
import logging
from watchdog.observers import Observer
from watchdog.events import LoggingEventHandler

if __name__ == "__main__":
    logging.basicConfig(level=logging.INFO,
                        format='%(asctime)s - %(message)s',
                        datefmt='%Y-%m-%d %H:%M:%S')
    path = sys.argv[1] if len(sys.argv) > 1 else '.'
    event_handler = LoggingEventHandler()
    observer = Observer()
    observer.schedule(event_handler, path, recursive=True)
    observer.start()
    try:
        while True:
            time.sleep(1)
    except KeyboardInterrupt:
        observer.stop()
    observer.join()
    
//watchdog.events.FileSystemEventHandler   处理器基类 使用需要继承该类
class LoggingEventHandler(FileSystemEventHandler):# watchdog.events.LoggingEventHandler 自带的已实现子类
    """Logs all the events captured."""

    def on_moved(self, event):
        super(LoggingEventHandler, self).on_moved(event)

        what = 'directory' if event.is_directory else 'file'
        logging.info("Moved %s: from %s to %s", what, event.src_path,
                     event.dest_path)

    def on_created(self, event):
        super(LoggingEventHandler, self).on_created(event)

        what = 'directory' if event.is_directory else 'file'
        logging.info("Created %s: %s", what, event.src_path)

    def on_deleted(self, event):
        super(LoggingEventHandler, self).on_deleted(event)

        what = 'directory' if event.is_directory else 'file'
        logging.info("Deleted %s: %s", what, event.src_path)

    def on_modified(self, event):
        super(LoggingEventHandler, self).on_modified(event)

        what = 'directory' if event.is_directory else 'file'
        logging.info("Modified %s: %s", what, event.src_path)
```

*  self.on_any_event(event) ： 任何事件发生都会首先执行该方法，该方法默认为空，dispatch()方法会先执行该方法，然后再把event分派给其他方法处理 

* observer

  >  watchdog.observers.Observer(timeout=1) 
  >
  >  observer.schedule(event_handler, path, recursive=False) # 控指定路径path，该路径触发任何事件都会调用event_handler来处理，如果path是目录，则recursive=True则会递归监控该目录的所有变化。 