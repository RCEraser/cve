SQL injection vulnerability exists in ibos oa

official website：http://www.ibos.com.cn/

version:4.5.5

Function point: Background management = "Address book management =" Post management = "Delete post function office
![WPS图片(1)](https://github.com/RCEraser/cve/assets/131632691/7e2c164b-fc2a-492b-8fcf-b3415c0e3265)

POC

Route: r=dashboard/position/del

The injection parameter id exists

If the input is normal, the following information is displayed
![WPS图片(2)](https://github.com/RCEraser/cve/assets/131632691/9dd187c3-9b68-43a0-ab17-b6accc8cc669)
Stack delay successful
![WPS图片(3)](https://github.com/RCEraser/cve/assets/131632691/c9522a07-78af-4238-ad9f-3eb8d27e5f21)
The module layer deleteAll() method is invoked through the actionDel() method to execute the SQL statement.
![WPS图片(4)](https://github.com/RCEraser/cve/assets/131632691/6947a225-81c0-4f9d-a665-e07a9bec97d7)
![WPS图片(5)](https://github.com/RCEraser/cve/assets/131632691/b7b2e03d-3d8f-476d-9c31-93b06ae60eff)
![WPS图片(6)](https://github.com/RCEraser/cve/assets/131632691/7f921357-a407-4427-af22-bddc3446e57b)
