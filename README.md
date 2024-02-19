- 👋 Hi, I’m @Hackbacknow
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
Hackbacknow/Hackbacknow is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
if [[ -z "${1}" || -z "${2}" ]]; then
  echo "Error: missing arguments"
  exit 1
fi

if [[ ! -f beef || ! -f VERSION ]]; then
  echo "Error: must be run from within the BeEF root directory"
  exit 1
fi

echo "Updating version ${1} to ${2}"

git checkout -b "release/${2}"
sed -i '' -e "s/$1/$2/g" VERSION
sed -i '' -e "s/\"version\": \"$1\"/\"version\": \"$2\"/g" package.json
sed -i '' -e "s/\"version\": \"$1\"/\"version\": \"$2\"/g" package-lock.json
sed -i '' -e "s/\"version\": \"$1\"/\"version\": \"$2\"/g" config.yaml

git add VERSION package.json package-lock.json config.yaml
git commit -m "Version bump ${2}"
git push --set-upstream origin "release/${2}"
git push
