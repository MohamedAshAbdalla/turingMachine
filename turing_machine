#MohamedAbdalla
#Date:2016-12-05
#Using Python 3 
#TuringMachine
import fileinput
import os

#Parse the action table from the file
#Input: File content
#Output: Returns the action table list 
def action_table(content):
	action_list = []
	for action in content:
		if len(action) > 1:
			action_list.append(action)
	return action_list

#Get the initial parameters before the action table
#Input: File content
#Output: Returns the offset, starting state index and the halting state
def get_parameters(content):
	offset = content[1][0]
	start_index = content[2][0]
	halting_state = content[3][0]
	print ("Offset: " + str(offset))
	print ("Starting State: " + str(start_index))
	print ("Halting State: " + str(halting_state), "\n" )
	return offset,start_index,halting_state

#Splitting the content into a list so we can move the header
#Input: File content
#Output: Returns the tape content 
def get_contents(content):
	start_contents = list (content[0][0])
	print ("Tape Content is: " + content[0][0])
	return start_contents

#Putting the content of the file into a 2D-Array
#Remove the new line character (1st array) then split based on whitespace (2nd array)
#Reads the file and returns the content of the file
def read_file():
	 content = []
	 fileIns = fileinput.input()

	 try:
	 	for line in fileIns:
	 		content.append(line.rstrip('\n').split())
	 except IOError:
	 	print ("The file" + fileinput.filename() + " does not exist. Exiting the program. Please check that the file is in the correct directory.")
	 	return 1

	 #Check if the file in Empty
	 if os.path.getsize(fileinput.filename()) == 0:
	 	print ("The " + fileinput.filename() + " is empty. Please Add the file with correct format.") 
	 	return 1

	 return content

#Update the header position and the state
#Input: Takes in the current header_position direction and next_state
#Output: Returns the new header position and current state 
def update_position_and_state(header_position,direction,next_state):
	header_new_position= header_position+int(direction)
	current_state = next_state
	return header_new_position,current_state

#Check the formating of the File
#Input:Takes the file content and action table list 
#Output: returns 1 if any fault was found else 0 if format is correct
def check_format(content,action_list):

	if len(content[0]) > 1 or len(content[1]) > 1 or len(content[2]) > 1 or len(content[3]) > 1:
		print ("The format is wrong for the files. Please make sure that there are no spaces in first 4 lines of the file")
		return 1

	for line in action_list:
		if len (line) != 5 :
			print ("The format for the action table is wrong")
			return 1

def main():
	print ("\n", "###################### Starting the Turing Machine ###################################", "\n")
	content = read_file()
	if content == 1: return 1

	action_list = action_table(content)
	if check_format(content,action_list) == 1: return 1

	start_contents = get_contents(content)
	offset,start_index,halting_state = get_parameters(content)
	

	header_position = int (offset)
	current_state = start_index
	notHalt = True

	while notHalt:

		header_content = start_contents[header_position]
		print ("The header is at: " + header_content)

		for move in action_list:
			if current_state == move[0] and (header_content == move[1] or move[1] == "*"):
				if move[2] == "*":
					print ("There is a wild card. The content stays the same: " + header_content)
					header_position,current_state = update_position_and_state(header_position,move[3],move[4])
					print ("The current conversion is: " + "".join(start_contents), "\n")
					break

				start_contents[header_position] = move[2]
				header_position,current_state = update_position_and_state(header_position,move[3],move[4])
				print ("The current conversion is: " + "".join(start_contents))
				print ("The content is replaced with: " + move[2])
				print ("The new header position is: " + str(header_position))
				print ("The new state is: " + current_state, "\n")
				break

			elif current_state == halting_state:
				print ("Halting state " + current_state + " reached!. Stopping the Turing Machine.", "\n")
				notHalt = False
				break

		#If the end of the content tape is reached then  "-" is added representing a blank space
		#because the tap is infinite
		try:
		 start_contents[header_position]
		except IndexError:
			start_contents.extend("-")

	print ("The Final conversion is: " + "".join(start_contents))
	return 0 

main()