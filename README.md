#!/usr/bin/env python3
"""
Launch script for Mycorrhizal Image Annotator
"""

import os
import sys
import subprocess

def install_dependencies():
    """Install required packages"""
    print("📦 Installing annotation tool dependencies...")
    
    packages = [
        "streamlit>=1.25.0",
        "pillow>=9.0.0", 
        "pandas>=1.5.0",
        "numpy>=1.21.0",
        "opencv-python-headless>=4.6.0",
        "streamlit-drawable-canvas>=0.9.0"
    ]
    
    for package in packages:
        try:
            subprocess.run([sys.executable, "-m", "pip", "install", package], 
                          check=True, capture_output=True)
            print(f"   ✅ {package.split('>=')[0]}")
        except subprocess.CalledProcessError:
            print(f"   ⚠️ Failed to install {package.split('>=')[0]}")

def create_directories():
    """Create necessary directories"""
    print("📁 Setting up annotation workspace...")
    
    directories = [
        "uploaded_images",
        "annotations/masks",
        "annotations/metadata", 
        "export"
    ]
    
    for directory in directories:
        os.makedirs(directory, exist_ok=True)
        print(f"   ✅ {directory}")

def launch_annotator():
    """Launch the annotation website"""
    print("\n🚀 Launching Mycorrhizal Image Annotator...")
    print("🔬 Professional annotation tool for microscopy images")
    print("📱 Access the tool at the forwarded port 8501")
    
    try:
        subprocess.run([
            "streamlit", "run", "mycorrhizal_annotator.py",
            "--server.port=8501",
            "--server.address=0.0.0.0",
            "--browser.gatherUsageStats=false"
        ])
    except KeyboardInterrupt:
        print("\n👋 Annotation tool stopped")
    except FileNotFoundError:
        print("❌ Streamlit not found. Install with: pip install streamlit")

def main():
    """Main execution"""
    print("🔬 MYCORRHIZAL IMAGE ANNOTATOR")
    print("=" * 40)
    print("Professional annotation tool for AI training")
    print("=" * 40)
    
    # Setup
    install_dependencies()
    create_directories()
    
    # Launch
    launch_annotator()

if __name__ == "__main__":
    main()
