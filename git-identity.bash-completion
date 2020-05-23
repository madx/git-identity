# vim: ft=sh:
# shellcheck disable=SC2154
_git_identity () {
	# Needs the bash-completion for git proper
	[ -n "$__git_whitespacelist" ] || return;

	_get_comp_words_by_ref -n =: cur words
	# git identity -h | tr '|' '\n'|grep -oE '\-.+'|cut -f1 -d']' |tr '\n' ' '
	# The grep regex is a bit hack-y, but this is just over-optimizing anyway
	# Whenever you add more commands just come add them here
	local commands="-d --define --define-gpg --define-ssh -p --print -s --get-settings -r --remove -l --list -R --list-raw -u --update -h -c --get-shell-command"

	case "$cur" in
		-*)
			__gitcomp "$commands"
		;;
		*)
			__gitcomp "$(git identity --list-raw)"
		;;
	esac
}
