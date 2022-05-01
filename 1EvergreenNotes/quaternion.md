# quaternion

Quaternion is 4 component vector which is an axis and an angle of rotation around this axis.
Euler rotation is basically applies by gimbal machine.

![[Pasted image 20220209195428.png]]

Problems of the auler angles are
 - Ambiguity. You do not know weather it is X Y Z ot Y Z X or anything else.
 - Gimbal lock. [[Gimble Lock Video]] Two coordinates may result in the same transformation. Some strange trajectory might appear when you want to rotate an object.

#programming/gamedev #interview 
