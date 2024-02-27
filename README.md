# 项目介绍

ssm支教管理系统（前台+后台） 

前台角色：支教学校+志愿者 

支教学校功能模块：支教学校查询+报名职位+发布+已发布列表+已报名列表+评论列表+联系管理员+信息管理 

志愿者功能模块：支教学校查询+报名职位+参与职位+我的评价+支教服务时长+信息管理 

后台角色：管理员 

功能模块：管理员管理+志愿者管理+支教学校管理+志愿者管理+报名审核+职位管理+轮播图设置+评论管理+留言管理

环境：IDEA+jdk1.8+Tomcat9+MySQL5.7+maven3.6.1 

技术：ssm+jsp 



# 环境要求

1.运行环境：最好是java jdk1.8,我们在这个平台上运行的。其他版本理论上也可以。 

2.IDE环境：IDEA,Eclipse,Myeclipse都可以。推荐IDEA; 

3.tomcat环境：Tomcat7.x,8.X,9.x版本均可 

4.硬件环境：windows7/8/10 4G内存以上；或者Mac OS; 

5.是否Maven项目：是；查看源码目录中是否包含pom.xml;若包含，则为maven项目，否则为非maven.项目 

6.数据库：MySql5.7/8.0等版本均可；

# 技术栈

后台框架：springmvc、MyBatis

数据库：MySQL

环境：JDK8、TOMCAT、IDEA

# 使用说明

1.使用Navicati或者其它工具，在mysql中创建对应sq文件名称的数据库，并导入项目的sql文件； 

2.使用IDEA/Eclipse/MyEclipse导入项目，修改配置，运行项目； 

3.将项目中config-propertiesi配置文件中的数据库配置改为自己的配置，然后运行；

# 运行指导

idea导入源码空间站顶目教程说明(Vindows版)-ssm篇：

http://mtw.so/5MHvZq 

源码看好后直接在网站付款下单即可，付款成功会自动弹出百度网盘链接，网站地址：[http://codegym.top](http://codegym.top/)。 

其它问题请关注公众号：**IT小舟**,关注后发送消息即可，都会给您回复的。若没有及时回复请耐心等待，通常当天会有回复

# 运行截图

## 前端界面

![O1CN01tPMWKS28H08diFPgX_!!0-fleamarket.jpg_q50.jpg_](https://gulimallcativen.oss-cn-shenzhen.aliyuncs.com/bishe/O1CN01tPMWKS28H08diFPgX_!!0-fleamarket.jpg_q50.jpg_.jpg)



![O1CN01yniudB28H08lBMku4_!!0-fleamarket.jpg_q50](https://gulimallcativen.oss-cn-shenzhen.aliyuncs.com/bishe/O1CN01yniudB28H08lBMku4_!!0-fleamarket.jpg_q50.jpg)

## ![O1CN01bAb8La28H08gUYBbP_!!0-fleamarket.jpg_q50](https://gulimallcativen.oss-cn-shenzhen.aliyuncs.com/bishe/O1CN01bAb8La28H08gUYBbP_!!0-fleamarket.jpg_q50.jpg)

![O1CN01jEhmm028H08fNHjMc_!!0-fleamarket.jpg_q50](https://gulimallcativen.oss-cn-shenzhen.aliyuncs.com/bishe/O1CN01jEhmm028H08fNHjMc_!!0-fleamarket.jpg_q50.jpg)

![O1CN01LbjvIX28H08aw3gyI_!!0-fleamarket.jpg_q50](https://gulimallcativen.oss-cn-shenzhen.aliyuncs.com/bishe/O1CN01LbjvIX28H08aw3gyI_!!0-fleamarket.jpg_q50.jpg)

## 后台界面

![O1CN01T3o2jS28H08in7qcT_!!0-fleamarket.jpg_q50](https://gulimallcativen.oss-cn-shenzhen.aliyuncs.com/bishe/O1CN01T3o2jS28H08in7qcT_!!0-fleamarket.jpg_q50.jpg)

![O1CN01ydwzCX28H08hAIDk6_!!0-fleamarket.jpg_q50](https://gulimallcativen.oss-cn-shenzhen.aliyuncs.com/bishe/O1CN01ydwzCX28H08hAIDk6_!!0-fleamarket.jpg_q50.jpg)

![O1CN012qTI3O28H08hAJMPN_!!0-fleamarket.jpg_q50](https://gulimallcativen.oss-cn-shenzhen.aliyuncs.com/bishe/O1CN012qTI3O28H08hAJMPN_!!0-fleamarket.jpg_q50.jpg)

![O1CN01ASobLY28H08jI6UzH_!!0-fleamarket.jpg_q50](https://gulimallcativen.oss-cn-shenzhen.aliyuncs.com/bishe/O1CN01ASobLY28H08jI6UzH_!!0-fleamarket.jpg_q50.jpg)

# 代码

UsersController

```java
package com.sys.lawyer.controller;

import com.alibaba.fastjson.JSONObject;
import com.github.pagehelper.PageHelper;
import com.sys.lawyer.base.BaseController;
import com.sys.lawyer.po.Releases;
import com.sys.lawyer.po.Users;
import com.sys.lawyer.service.UsersService;
import com.sys.lawyer.utils.Base64Img;
import com.sys.lawyer.utils.Pager;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.ResponseBody;
import org.springframework.web.multipart.MultipartFile;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.File;
import java.io.IOException;
import java.util.List;

/**
 * @ClassName:  
 * @Description: 
 * @author  - - admin
 * @date - 2018年10月17日 14时41分30秒
 */


@Controller
@RequestMapping("/users")
public class UsersController extends BaseController {
    
    
    /**
     * 依赖注入 start dao/service/===
     */
    @Autowired
    private UsersService usersService;
    
    /**
     * 【不分页 => 查询列表 => 无条件】
    * @Title: listAll 
    * @Description: TODO(这里用一句话描述这个方法的作用) 
    * @param @return 设定文件 
    * @author
    * @return String 返回类型 
    * @throws
     */
    @RequestMapping(value = "/listAll.json")
    @ResponseBody
    public String listAll(Users users, Integer pageIndex){
       PageHelper.startPage(notEmpty(pageIndex) ? pageIndex : 0, 15);
       Pager<Users> pagers = usersService.findByEntity(users);
       JSONObject jsonObject = new JSONObject();
       jsonObject.put("page", pagers);
       return jsonObject.toJSONString();
    }

    @RequestMapping(value = "getUser.json")
    @ResponseBody
    public String getUser(){
       JSONObject jsonObject = new JSONObject();
       if (notEmpty(usersService.getUser())){
          jsonObject.put("user", false);
       } else {
          jsonObject.put("user", false);
       }
       return jsonObject.toJSONString();
    }

    @RequestMapping(value = "list.do")
    public String list(Integer role, Model model){
       model.addAttribute("role", role);
       model.addAttribute("user", new JSONObject().toJSONString(usersService.getUser()));
       return "users/list";
    }

    /**
     *  【不分页=》查询列表=>有条件】
    * @Title: listByEntity 
    * @Description: TODO(这里用一句话描述这个方法的作用) 
    * @param @return 设定文件 
    * @author
    * @return String 返回类型 
    * @throws
     */
    @RequestMapping(value = "/listByEntity")
    public String listByEntity(Users users, Model model, HttpServletRequest request, HttpServletResponse response){
       List<Users> listAll = usersService.listAllByEntity(users);
       model.addAttribute("list", listAll);
       return "users/list";
    }

    @RequestMapping(value = "edit.do")
    @ResponseBody
    public String edit(Users users){
       Users users1 = usersService.getByEntity(users);
       JSONObject jsonObject = new JSONObject();
       jsonObject.put("bean", users1);
       return jsonObject.toJSONString();
    }

    @RequestMapping(value = "grxx.do")
    @ResponseBody
    public String grxx(){
       Users users1 = usersService.getUser();
       JSONObject jsonObject = new JSONObject();
       jsonObject.put("bean", users1);
       return jsonObject.toJSONString();
    }

    /**
     * 分页查询 返回list对象(通过对象)
     *
     * @return
     */
    @RequestMapping(value = "/findByObj")
    public String findByObj(Users users, Model model) {
       //分页查询
       Pager<Users> pagers = usersService.findByEntity(users);
       model.addAttribute("pagers", pagers);
       //存储查询条件
       model.addAttribute("bean", users);
       return "users/list";
    }

    /**
     * 跳至添加页面
     * @return
     */
    @RequestMapping(value = "/add")
    public String add() {
       return "users/addexcl";
    }

    @RequestMapping(value = "/zc")
    public String zc() {
       return "users/add";
    }

    @RequestMapping(value = "importExcl.do")
    public String importExcl() {
       return "users/addexcl";
    }

    @RequestMapping(value = "/importsave.json")
    @ResponseBody
    public String importsave(@RequestParam(value = "file", required = false) MultipartFile file, HttpServletRequest request) {
       JSONObject jsonObject = new JSONObject();
       boolean flag = false;
       if (notEmpty(file)){
          flag = usersService.importsave(file);
       }
       jsonObject.put("message", flag ? "提交成功" : "登录名重复或其他数据异常");
       jsonObject.put("flag", flag);
       return jsonObject.toJSONString();
    }

    @RequestMapping(value = "/reportExcl.do")
    public void reportExcl(Users users, HttpServletResponse response) {
       usersService.reportExcl(users, response);
    }
    
    /**
     * 添加执行
     * @return
     */
    @RequestMapping(value = "/exAdd")
    public String exAdd(Users users, @RequestParam(value = "file", required = false) MultipartFile file, String openid) throws IOException {
       if (file.getSize() > 0){
          String str = Base64Img.getImgStr(file.getInputStream());
          String type = file.getContentType();
          users.setPhoto("data:" + type + ";base64," + str);
       }
       usersService.insert(users);
       return "redirect:/users/findByObj";
    }

    @RequestMapping(value = "/update.json")
    @ResponseBody
    public String update(Users users, @RequestParam(value = "file", required = false) MultipartFile file, HttpServletRequest request) {
       JSONObject jsonObject = new JSONObject();
       Users user = usersService.getUser();
       Users users1 = usersService.getById(user.getId());
       if (user.getRole() == 1 || user.getRole() == 0){
          if (notEmpty(users)){
             if (notEmpty(users.getId())){
                if (notEmpty(file)){
                   users.setPhoto("/resource/upload/" + saveFile(file, request));
                }
                users.setIsDelete(0);
                usersService.updateById(users);
                if (user.getId() == users.getId()){
                   request.getSession().setAttribute("user", usersService.getById(users.getId()));
                }
             }
             jsonObject.put("message", "提交成功");
             jsonObject.put("flag", true);
          }
       } else if ((user.getRole() > 1) || (notEmpty(users1) && user.getRole() == 1 && users1.getRole() == 0)){
          jsonObject.put("message", "权限不足");
          jsonObject.put("flag", false);
       }
       return jsonObject.toJSONString();
    }

    @RequestMapping(value = "/updateGrxx.json")
    @ResponseBody
    public String updateGrxx(Users users, @RequestParam(value = "file", required = false) MultipartFile file, HttpServletRequest request) {
       JSONObject jsonObject = new JSONObject();
       if (notEmpty(users)){
          if (notEmpty(users.getId())){
             if (notEmpty(file)){
                users.setPhoto("/resource/upload/" + saveFile(file, request));
             }
             users.setIsDelete(0);
             usersService.updateById(users);
             request.getSession().setAttribute("user", usersService.getById(users.getId()));
          }
          jsonObject.put("message", "修改成功");
          jsonObject.put("flag", true);
       }
       return jsonObject.toJSONString();
    }

    @RequestMapping(value = "/save.json")
    @ResponseBody
    public String save(Users users, @RequestParam(value = "file", required = false) MultipartFile file, HttpServletRequest request) {
       JSONObject jsonObject = new JSONObject();
       Users user = usersService.getUser();
       Users users1 = new Users();
       if (user.getRole() == 1 || user.getRole() == 0){
          if (notEmpty(users)){
             users1.setName(users.getName());
             users1 = usersService.getByEntity(users1);
             if (notEmpty(users1)){
                jsonObject.put("message", "登录名重复");
                jsonObject.put("flag", false);
             } else {
                users.setPhoto("/resource/upload/" + saveFile(file, request));
                users.setIsDelete(0);
                if (notEmpty(users.getId())){
                   usersService.update(users);
                } else {
                   usersService.insert(users);
                }
//              request.getSession().setAttribute("user", users);
                jsonObject.put("message", "提交成功");
                jsonObject.put("flag", true);
             }
          }
       } else {
          jsonObject.put("message", "权限不足");
          jsonObject.put("flag", false);
       }
       return jsonObject.toJSONString();
    }


    /**
     * 删除通过主键
     * @return
     */
    @RequestMapping(value = "delete.json")
    @ResponseBody
    public String delete(Integer id) {
       Users users = usersService.getUser();
       Users users2 = usersService.getById(id);
       JSONObject jsonObject = new JSONObject();
       if (users.getRole() == 0 || users.getRole() == 1){
          if (users.getId() == id){
             jsonObject.put("flag", false);
             jsonObject.put("message", "不能删除自己");
          } else if (users.getRole() ==1 && users2.getRole() == 0){
             jsonObject.put("flag", false);
             jsonObject.put("message", "不能删除超级管理员");
          } else {
             usersService.deleteById(id);
             jsonObject.put("flag", true);
             jsonObject.put("message", "删除成功");
          }
       } else {
          jsonObject.put("flag", false);
          jsonObject.put("message", "本账号无权限删除用户");
       }
       return jsonObject.toJSONString();
    }

    @RequestMapping(value = "sh.json")
    @ResponseBody
    public String sh(Integer id) {
       JSONObject jsonObject = new JSONObject();
       Users users = usersService.getById(id);
       users.setIsSh(1);
       usersService.updateById(users);
       jsonObject.put("flag", true);
       jsonObject.put("message", "审核成功");
       return jsonObject.toJSONString();
    }

    /**
     * 【不分页 => 查询列表 => 无条件】
    * @Title: listAll 
    * @Description: TODO(这里用一句话描述这个方法的作用) 
    * @param @return 设定文件 
    * @author
    * @return String 返回类型 
    * @throws
     */
    @RequestMapping(value = "/listAllJson", method = RequestMethod.POST)
    @ResponseBody
    public String listAllJson(Users users, HttpServletRequest request, HttpServletResponse response){
       List<Users> listAll = usersService.listAll();
       JSONObject jsonObject = new JSONObject();
       jsonObject.put("list", listAll);
       jsonObject.put("obj", users);
       return jsonObject.toString();
    }
    
    /**
     * ajax 添加
     * @param 
     * @return
     */
    @RequestMapping(value = "/exAddJson", method = RequestMethod.POST)
    @ResponseBody
    public String exAddJson(Users users, HttpServletRequest request, HttpServletResponse response) {
       usersService.insert(users);
       JSONObject jsonObject = new JSONObject();
       jsonObject.put("message", "添加成功");
       return jsonObject.toString();
    }
    

    /**
     * ajax 修改
     * @param 
     * @return
     */
    @RequestMapping(value = "/exUpdate.json", method = RequestMethod.POST)
    @ResponseBody
    public String exUpdateJson(Users users, Model model, HttpServletRequest request, HttpServletResponse response) {
       //1.通过实体类修改，可以多传修改条件
       usersService.update(users);
       //2.通过主键id修改
       //usersService.updateById(users);
       JSONObject jsonObject = new JSONObject();
       jsonObject.put("message", "修改成功");
       return jsonObject.toString();
    }


    @RequestMapping(value = "loginOut.do")
    public String loginOut(HttpServletRequest request){
       request.getSession().removeAttribute("user");
       return "redirect:/web/index.do";
    }

    public String saveFile(@RequestParam(value = "file", required = false) MultipartFile files, HttpServletRequest request) {
       String filePath = "";
       String fileNmae = "";
       if (notEmpty(files)) {
          int pre = (int) System.currentTimeMillis();
          try {
             filePath = request.getRealPath("/resource/upload/");
             File f = new File(filePath);
             if (!f.exists()) {
                f.mkdirs();
             }
             fileNmae = pre + files.getOriginalFilename().replaceAll(" ", "").replace("(", "").replace(")", "");
             File file = new File(filePath + fileNmae);
             if (!file.exists()) {
                file.createNewFile();
             }
             files.transferTo(file);
          } catch (Exception e) {
             e.printStackTrace();
             System.out.println("上传出错");
          }
       }
       return fileNmae;
    }
}
```
