import numpy as np
import cv2
import argparse
from collections import deque
from pathlib import Path

#c_path = Path.cwd() / Path("chromedriver")
#print('c_path',c_path)

c_path='chromedriver.exe'

from agora_community_sdk import AgoraRTC
client = AgoraRTC.create_watcher("49c2343ef91c4517a6c6a93a445e0a43", str(c_path))
client.join_channel("gesture")

users = client.get_users() # Gets references to everyone participating in the call

for i in range(len(users)):
        user1 = users[i] # Can reference users in a list

        print('-----user1------',user1)

        #cap=cv2.VideoCapture(0)

        binary_image = user1.frame.convert("RGB") # Gets the latest frame from the stream as a PIL image
        binary_image.save("test.jpeg", "jpeg")

        pts = deque(maxlen=64)

        Lower_green = np.array([24,50,50])
        Upper_green = np.array([42,255,255])

        while True:
                binary_image = user1.frame.convert("RGB") # Gets the latest frame from the stream as a PIL image
                img = np.asarray(binary_image)[:,:,:3][:,:,::-1].copy()
                hsv=cv2.cvtColor(img,cv2.COLOR_BGR2HSV)
                kernel=np.ones((5,5),np.uint8)
                mask=cv2.inRange(hsv,Lower_green,Upper_green)
                mask = cv2.erode(mask, kernel, iterations=2)
                mask=cv2.morphologyEx(mask,cv2.MORPH_OPEN,kernel)
                #mask=cv2.morphologyEx(mask,cv2.MORPH_CLOSE,kernel)
                mask = cv2.dilate(mask, kernel, iterations=1)
                res=cv2.bitwise_and(img,img,mask=mask)
                cnts,heir=cv2.findContours(mask.copy(),cv2.RETR_EXTERNAL,cv2.CHAIN_APPROX_SIMPLE)[-2:]
                center = None
        
                if len(cnts) > 0:
                        c = max(cnts, key=cv2.contourArea)
                        ((x, y), radius) = cv2.minEnclosingCircle(c)
                        M = cv2.moments(c)
                        center = (int(M["m10"] / M["m00"]), int(M["m01"] / M["m00"]))
        
                        if radius > 5:
                                cv2.circle(img, (int(x), int(y)), int(radius),(0, 255, 255), 2)
                                cv2.circle(img, center, 5, (0, 0, 255), -1)
                        
                pts.appendleft(center)
                for i in range (1,len(pts)):
                        if pts[i-1]is None or pts[i] is None:
                                continue
                        thick = int(np.sqrt(len(pts) / float(i + 1)) * 2.5)
                        cv2.line(img, pts[i-1],pts[i],(0,0,225),thick)
                        
                
                cv2.imshow("Frame", img)
                cv2.imshow("mask",mask)
                cv2.imshow("res",res)
                
                
                k=cv2.waitKey(75) & 0xFF
                if k==32:
                break;
        # cleanup the camera and close any open windows

#cap.release()
cv2.destroyAllWindows()
client.unwatch()# Stop listening to the channel. Not calling this can cause memory leaks
