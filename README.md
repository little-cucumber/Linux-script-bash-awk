# Linux-script-bash-awk
This is a record for my linux class notes.
Work of Tianyi Huang.
Indicate the citation if copy the whole Code.
-------------------------------------------------------------------------------------------------------------------------------------------
------AWK Script------Use one awk to deal with multiple files. Find key words, count number...------------------------------------------
#!/bin/bash
awk 'BEGIN{
}
{
	if (FILENAME ~ /^[input]/){
		if($2 ~ /^[0-9]/){
			arrayWeight[$1]
		}
		else{
			$1 = $1" "$2;
			$2 = $3;
		}
		if($1 == "c++" || $1 == "C++"){
			$1 = "c\+\+"
		}
		arrayWeight[$1]=$2
	}
	else{
		if(currentFile!=FILENAME ){
			currentFile=FILENAME
			name = currentFile
			gsub("submissions\/","",name)
			arrayScore[name] = 0
			

		}
		else{
			specialString = tolower($0)
			# print(specialString)
			gsub(" ","",specialString)
			for (itemName in arrayWeight){
				lowIN = tolower(itemName)
				gsub(" ","",lowIN)
				while(match(specialString,lowIN)){
					if(lowIN == "c++" || $1 == "C++"){
						lowIN = "c\+\+"
					}
					arrayScore[name] += arrayWeight[itemName]
					sub(lowIN,"",specialString)				
				}
			}
		}
	}
}
END{
	for(name in arrayScore){
		print arrayScore[name]" "name | "sort -nr -k1"
	}
}' input.txt submissions/*

----------------------------------------------------------------------------------------------------------------------------------------
