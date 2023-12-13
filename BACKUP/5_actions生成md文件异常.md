# [actions生成md文件异常](https://github.com/Smileye-v/gitblog/issues/5)

测试

---

![image](https://user-images.githubusercontent.com/68359161/226306607-2738eea5-f6e4-4ac4-8523-e9915c869aca.png)
报403错误，提示没有权限
修改权限为可读写后执行正常
![image](https://user-images.githubusercontent.com/68359161/226306805-604b747f-525f-44fb-ac11-d43c3d9b1dfc.png)


---

401 错误
生成文件设置的 Actions secrets 有效期限到期，更新后正常

---

报错信息：Run source venv/bin/activate
Traceback (most recent call last):
  File "main.py", line 305, in <module>
    main(options.github_token, options.repo_name, options.issue_number)
  File "main.py", line 271, in main
    func(repo, "README.md", me)
  File "main.py", line 203, in add_md_label
    issues = get_issues_from_label(repo, label)
  File "main.py", line 117, in get_issues_from_label
    return repo.get_issues(labels=(label,))
  File "/home/runner/work/gitblog/gitblog/venv/lib/python3.8/site-packages/github/Repository.py", line 2813, in get_issues
    assert is_optional_list(labels, (github.Label.Label, str)), labels
AssertionError: (Label(name="杂七杂八"),)
Error: Process completed with exit code 1.

解决方法：
 问题出现在 main.py 的 get_issues_from_label 函数中，具体在调用 repo.get_issues(labels=(label,)) 这一行。错误是一个 AssertionError，表明 labels 参数不符合 get_issues 方法所期望的格式。
在 github 库中，get_issues 方法的 labels 参数应该是一个列表，其中包含字符串或 github.Label.Label 对象。您的错误消息显示，传递的是一个包含单个 Label 对象的元组 (Label(name="杂七杂八"),)。
要修复这个问题，您应该将 labels 参数修改为一个列表，即使只有一个标签。如果 label 是一个 github.Label.Label 对象或字符串，正确的调用方式应该是：
`return repo.get_issues(labels=[label])`
在 get_issues_from_label 函数中做这样的修改应该能解决问题。这样可以确保即使只有一个标签，它也被正确地包装在一个列表中，从而符合 get_issues 方法的期望参数格式。