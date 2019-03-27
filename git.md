# git

# 删除本地commit的大文件100MB

  git filter-branch --index-filter 'git rm --cached --ignore-unmatch 文件路径' 合并的commitID..HEAD
  
  
