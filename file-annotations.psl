
# Default annotation store location under user's home directory
$ANNOTATION_DIR = Join-Path $HOME ".file-annotations"

function ls-tip {
    # Get all files in current directory
    $files = Get-ChildItem

    # Load all annotations
    $annotations = @{}
    if (Test-Path $ANNOTATION_DIR) {
        Get-ChildItem $ANNOTATION_DIR -Filter "*.txt" | ForEach-Object {
            $annotation = Get-Content $_.FullName | ConvertFrom-Json
            # Convert the Path property to string if it's an object
            $pathString = if ($annotation.Path.Path) {
                $annotation.Path.Path  # Use the Path property if it exists
            } else {
                $annotation.Path.ToString()
            }
            $annotations[$pathString] = $annotation.Tip
        }
    }

    # Display files with their annotations
    $files | ForEach-Object {
        $fullPath = $_.FullName
        $annotation = $annotations[$fullPath]
        if ($annotation) {
            "$($_.Name) - $annotation"
        } else {
            $_.Name
        }
    }
}

function Set-FileInfoTip {
    param (
        [string]$FileName,
        [string]$InfoTip
    )
    
    # Create annotation directory if it doesn't exist
    if (-not (Test-Path $ANNOTATION_DIR)) {
        New-Item -ItemType Directory -Path $ANNOTATION_DIR | Out-Null
    }

    # Get absolute path of the target file
    $fullPath = (Resolve-Path $FileName).Path  # Get the string path
    # Create a hash of the full path to use as annotation file name
    $pathHash = [System.Convert]::ToBase64String([System.Text.Encoding]::UTF8.GetBytes($fullPath))
    $annotationFile = Join-Path $ANNOTATION_DIR "$pathHash.txt"

    # Store the annotation with the full path
    @{
        Path = $fullPath  # Store as string
        Tip = $InfoTip
    } | ConvertTo-Json | Set-Content $annotationFile
}

# Create aliases
New-Alias -Name tip -Value Set-FileInfoTip
New-Alias -Name lst -Value ls-tip
