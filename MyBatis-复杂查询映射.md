# 多对一的映射关系

## 方法1

```xml
    <resultMap id="student" type="com.chaoRen.bean.Student">
        <result column="id" property="id"/>
        <result column="name" property="name"/>
        <result column="age" property="age"/>
        <association property="teacher" column="t_id" javaType="com.chaoRen.bean.Teacher" select="getTeacher"/>
    </resultMap>

    <select id="getStudent" resultMap="student">
        select * from student
    </select>

    <select id="getTeacher" resultType="com.chaoRen.bean.Teacher">
        select * from teacher where id=#{tId}
    </select>
```

## 方法2

```xml
    <resultMap id="student2" type="com.chaoRen.bean.Student">
        <result column="sid" property="id"/>
        <result column="sname" property="name"/>
        <result column="sage" property="age"/>
        <association property="teacher" javaType="com.chaoRen.bean.Teacher">
            <result column="t_id" property="id"/>
            <result column="tname" property="name"/>
            <result column="tage" property="age"/>
        </association>
    </resultMap>

    <select id="getStudent2" resultMap="student2">
        select student.id sid,
               student.name sname,
               student.age sage,
               t_id,
               teacher.name tname,
               teacher.age tage
        from student,teacher
        where t_id=teacher.id
    </select>
```

---

---

# 一对多的映射关系

## 方法1

~~~xml
    <resultMap id="teacher1" type="com.chaoRen.bean.Teacher">
        <result column="t_id" property="id"/>
        <result column="tname" property="name"/>
        <result column="tage" property="age"/>
        <collection property="students" ofType="com.chaoRen.bean.Student">
            <result column="sid" property="id"/>
            <result column="sname" property="name"/>
            <result column="sage" property="age"/>
        </collection>
    </resultMap>

    <select id="getTeacher" resultMap="teacher1">
        select  t_id,
                teacher.name tname,
                teacher.age tage,
                student.id sid,
                student.name sname,
                student.age sage
        from teacher,student
        where teacher.id=#{sId}
    </select>
~~~

## 方法2

~~~xml
    <resultMap id="teacher2" type="com.chaoRen.bean.Teacher">
        <result column="id" property="id"/>
        <collection property="students" column="id" javaType="List" ofType="com.chaoRen.bean.Student" select="getStudents"/>
    </resultMap>

    <select id="getTeacher2" resultMap="teacher2">
        select * from teacher where id=#{tId}
    </select>

    <select id="getStudents" resultType="com.chaoRen.bean.Student">
        select * from student where t_id=#{tId}
    </select>
~~~

